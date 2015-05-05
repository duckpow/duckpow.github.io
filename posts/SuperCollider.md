
# Lessons learned from performing with SuperCollider

A few weeks back I was asked by a couple of friends to create some ambient textures to a spoken words session. Not wanting to be tied down by the sequencer of my DAW I choose SuperCollider as my tool. I performed with SuperCollider a few days back and that was my first experience using SC live. Everything worked beautifully with no crashes or odd behaviours, thou it took some time to get there:

Working with SuperCollider for a live performance proved to be very different from using a DAW or some other 'commercial'-hardware. And quite a lot harder.
In DAW's (made for live use) there is often one or two 'right ways' where as in SC, you have to invent your own way to perform your piece.
Because of this I had to plan out what I wanted to do a lot more than I would do normally.

The challenges I faced were not writing the sounds (SynthDef's) for the piece, which were done one at a time in small sketches, but more combining every aspect into one script.

# Live code
The way I have seen most SC performers work is with 'live coding'. Code is written and evaluated as needed during the performance. This is really awesome. However it has a few limitations:
> You can only type so fast. Needing a file for a buffer in a tenth subfolder takes a lot of time to write.
> One spelling error will either mean you code won't get evaluated in time or worse: The code does something unexpected to you.
> Keeping track of variables can be hard. SC has a great framework for live coding with proxies, patterns and busses. But I found that using the global variables quickly becomes a mess with a lot of variables you just don't need again. (I will come back to this)
> You are more prone to errors when you are under stress. I am in particular... Combine with any or all of the above and it would spell disaster.

For these reasons I choose to write all code in advance.

# What do you need
Though the code was written for sound visual feedback is nice. Both for controls and monitoring. SC's classes for writing GUI's is pleasantly flexible, but writing code for many different Synth's can quickly becomes repetitive.
I choose to avoid trying to 'design' a pretty interface and instead automate the process inspired by a method found in the SuperCollider book:
Accessing a synthdefs arguments can be done by looking it up in the Synth description Library 'SynthDescLib.global[\mySynth]'. This returns SynthDesc from which we can gain access to the arguments as an array of Strings using '.controlNames'. We could then create a Slider (or Dial or other similar) for each of theses, but we would be missing key data. Like what is the maximum and minimum allowed values. Luckily SC has a way to solve this problem: ControlSpec.
ControlSpec or just Spec, can hold (almost) all the data we would need to initialize our controller for any given SynthDef argument. The amount initialized by default is fairly low but this, as shown later, is actually a good thing. But we do need to register all arguments we want controls for as new ControlSpecs.
By calling '.asSpec' on a symbol we get the corresponding ControlSpec if one exist. Else we get 'nil'. This can be utilized when iterating over the controlNames from SynthDesc as all arguments whos symbol returns 'nil' when '.asSpec' is called can be discarded.

'EZSlider' takes it's mappings as a ControlSpec (hurray) and saving the slider in a Dictionary using the argument name as key will make referencing later easy.
Code:
```
sliderFabric{
	// create and bind sliders to a synth
	// Requires its parameters to be registered in ControlSpec. Skips otherwise
	arg synthName, myView;

	SynthDescLib.global[synhtName.asSymbol].controlNames.do({
		arg name, index;
		var spec, action;
		spec = name.asSymbol.asSpec;
		action = {|sl| synth.set(name.asSymbol, sl.value);};
		// synth (a Synth) needs to exist at least one scope higher
		spec.notNil.if({
			sliders.add(name -> EZSlider(
				myView,
				Rect(10+(sliders.size*50),vertOffset,30,180),
				name, spec, action, layout: 'vert'
			));
		});
	});
}
``

# Moving to classes
SC's strong object oriented nature makes it natural to keep a Synth and all its controls within one class instance. As far as I am aware SC does not have a class for this purpose so I had to write one myself.
Classes for SC is unfortunately lacking good tutorials but are not lacking in incredibly useful features. Looking back at my code my biggest regret is probably not making use of the fact that one Class definition can have multiple constructor methods. I made use of inheritance instead which is a concept I am more familiar with.
Having to recompile the class library (and by that effectively restarting SC) every time a change is made can be frustrating, but it can however help making sure your non-class code works as a single program.

# Making sure future me won't encounter (too many) errors
I have always thought of working with classes in a non-type-safe languages is inviting errors along. Reusing a class you wrote 10 months back and not remembering if it was ok to pass an integer or if it strictly needed a boolean will probably cause an error. Usually the error message is helpful, but with a little foresight one could write 'myBoolean = myBoolean.asBoolean;' which will turn any SimpleNumber accidentally cast to 'myBoolean' into a Boolean. A Boolean will return itself for the same reasons as 'nil.free' returns 'nil' and not an error.
The same is true for '.asSymbol' which is used a lot in my code. Reason being that SC's own Classes and methods often use them interchangeably.

# Not needing one monolithic MIDIdef
One thing I realised creating this performance was that for each parameter I needed midi controls I only needed a few arguments. Utilizing that one can do create as many MIDIdef as one would like as long as they are uniquely named, I create a method to my SuperClass which binds either a particular noteOn or CC message to a Slider or button. The unique name is guaranteed by concatenating the type with its response number. I.e: 'var defName = ("note" ++ number.asString).asSymbol;'

The MIDIdef's connects uses my Class' set method. Which connects to the GUI instead of directly to the Synth using .valueAction thus insuring the GUI is showing the values the Synth are using at any given time.
An interesting note here is SC's error message if the above action is not scheduled (Using AppClock or similar) which tells you can't change the Sliders value from this Thread.

# All parameters in one place
SC's collection of collections is very impressive.









Aktivitetsplan:
lvuhovedstaden@as3.dk