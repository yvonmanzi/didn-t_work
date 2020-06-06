How does flutter build UI?

I have broken Flutter down into four essential pieces for myself and anyone looking to get started learning this framework. Those are UI, backend, and state management. 

Today we will be talking about building UI. The part that the user sees and with which he does stuff(clicks, scrolls, etc).

If you are going to develop flutter apps, you will absolutely need to understand how flutter lays out its widgets. How does flutter determine where and how big a button is, for example? How big and where widgets are relative to other widgets. If you don’t understand this, then you will get stuck over and over. You will have the dreaded yellow and black stripes that will terrify the heck outta you if you are someone like me. So here’s how I learned it.

First of all, let’s look at the following code. I wrote it when I was trying to build a relatively simple ui before I learned how flutter works deep down.(the code that produces the error)


import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:flutterweather/src/blocs/blocs.dart';

import '../blocs/blocs.dart' as blocs;

class WeatherSearch extends StatefulWidget {
 @override
 _WeatherSearchState createState() => _WeatherSearchState();
}

class _WeatherSearchState extends State<WeatherSearch> {
 final _cityController = TextEditingController();
 WeatherBloc _weatherBloc;

 @override
 void initState() {
   super.initState();
   _weatherBloc = BlocProvider.of<WeatherBloc>(context);
 }

 @override
 Widget build(BuildContext context) {
   return Container(
     margin: EdgeInsets.symmetric(horizontal: 16.0),
     child: Row(
       mainAxisAlignment: MainAxisAlignment.spaceEvenly,
       children: <Widget>[
         TextFormField(
           controller: _cityController,
           decoration: InputDecoration(
             labelText: 'City',
             filled: true,
             hintText: 'City',
           ),
         ),
         SizedBox(
           width: 8.0,
         ),
         IconButton(
           icon: Icon(Icons.search),
           onPressed: () => _weatherBloc
               .add(blocs.WeatherSearch(cityName: _cityController.toString())),
         )
       ],
     ),
   );
 }
}










I/flutter ( 4259): ══╡ EXCEPTION CAUGHT BY RENDERING LIBRARY ╞═════════════════════════════════════════════════════════
I/flutter ( 4259): The following assertion was thrown during performLayout():
I/flutter ( 4259): An InputDecorator, which is typically created by a TextField, cannot have an unbounded width.
I/flutter ( 4259): This happens when the parent widget does not provide a finite width constraint. For example, if the
I/flutter ( 4259): InputDecorator is contained by a Row, then its width must be constrained. An Expanded widget or a
I/flutter ( 4259): SizedBox can be used to constrain the width of the InputDecorator or the TextField that contains it.
I/flutter ( 4259): 'package:flutter/src/material/input_decorator.dart':
I/flutter ( 4259): Failed assertion: line 945 pos 7: 'layoutConstraints.maxWidth < double.infinity'
I/flutter ( 4259): 
I/flutter ( 4259): Either the assertion indicates an error in the framework itself, or we should provide substantially
I/flutter ( 4259): more information in this error message to help you determine and fix the underlying cause.
I/flutter ( 4259): In either case, please report this assertion by filing a bug on GitHub:
I/flutter ( 4259):   https://github.com/flutter/flutter/issues/new?template=BUG.md
I/flutter ( 4259): 
I/flutter ( 4259): The relevant error-causing widget was:
I/flutter ( 4259):   TextFormField
I/flutter ( 4259):   file:///Users/yvonmanzi/AndroidStudioProjects/flutter_weather/lib/src/ui/weather_search.dart:29:11
I/flutter ( 4259): 
I/flutter ( 4259): When the exception was thrown, this was the stack:
I/flutter ( 4259): #2      _RenderDecoration._layout (package:flutter/src/material/input_decorator.dart:945:7)
I/flutter ( 4259): #3      _RenderDecoration.performLayout (package:flutter/src/material/input_decorator.dart:1262:44)
I/flutter ( 4259): #4      RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #5      RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #6      RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #7      RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #8      RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #9      RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #10     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #11     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #12     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #13     RenderFlex.performLayout (package:flutter/src/rendering/flex.dart:746:15)
I/flutter ( 4259): #14     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #15     RenderPadding.performLayout (package:flutter/src/rendering/shifted_box.dart:207:11)
I/flutter ( 4259): #16     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #17     MultiChildLayoutDelegate.layoutChild (package:flutter/src/rendering/custom_layout.dart:171:11)
I/flutter ( 4259): #18     _ScaffoldLayout.performLayout (package:flutter/src/material/scaffold.dart:484:7)
I/flutter ( 4259): #19     MultiChildLayoutDelegate._callPerformLayout (package:flutter/src/rendering/custom_layout.dart:240:7)
I/flutter ( 4259): #20     RenderCustomMultiChildLayoutBox.performLayout (package:flutter/src/rendering/custom_layout.dart:399:14)
I/flutter ( 4259): #21     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #22     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #23     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #24     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #25     _RenderCustomClip.performLayout (package:flutter/src/rendering/proxy_box.dart:1248:11)
I/flutter ( 4259): #26     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #27     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #28     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #29     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #30     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #31     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #32     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #33     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #34     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #35     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #36     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #37     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #38     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #39     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #40     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #41     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #42     RenderOffstage.performLayout (package:flutter/src/rendering/proxy_box.dart:3225:13)
I/flutter ( 4259): #43     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #44     _RenderTheatre.performLayout (package:flutter/src/widgets/overlay.dart:700:15)
I/flutter ( 4259): #45     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #46     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #47     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #48     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #49     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #50     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #51     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #52     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #53     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #54     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #55     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #56     RenderProxyBoxMixin.performLayout (package:flutter/src/rendering/proxy_box.dart:111:13)
I/flutter ( 4259): #57     RenderObject.layout (package:flutter/src/rendering/object.dart:1767:7)
I/flutter ( 4259): #58     RenderView.performLayout (package:flutter/src/rendering/view.dart:167:13)
I/flutter ( 4259): #59     RenderObject._layoutWithoutResize (package:flutter/src/rendering/object.dart:1630:7)
I/flutter ( 4259): #60     PipelineOwner.flushLayout (package:flutter/src/rendering/object.dart:887:18)
I/flutter ( 4259): #61     RendererBinding.drawFrame (package:flutter/src/rendering/binding.dart:402:19)
I/flutter ( 4259): #62     WidgetsBinding.drawFrame (package:flutter/src/widgets/binding.dart:884:13)
I/flutter ( 4259): #63     RendererBinding._handlePersistentFrameCallback (package:flutter/src/rendering/binding.dart:284:5)
I/flutter ( 4259): #64     SchedulerBinding._invokeFrameCallback (package:flutter/src/scheduler/binding.dart:1113:15)
I/flutter ( 4259): #65     SchedulerBinding.handleDrawFrame (package:flutter/src/scheduler/binding.dart:1052:9)
I/flutter ( 4259): #66     SchedulerBinding.scheduleWarmUpFrame.<anonymous closure> (package:flutter/src/scheduler/binding.dart:861:7)
I/flutter ( 4259): (elided 13 frames from class _AssertionError, class _RawReceivePortImpl, class _Timer, dart:async, and dart:async-patch)
I/flutter ( 4259): 
I/flutter ( 4259): The following RenderObject was being processed when the exception was fired: _RenderDecoration#e28b7 relayoutBoundary=up7 NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE:
I/flutter ( 4259):   creator: _Decorator ← InputDecorator ← AnimatedBuilder ← _PointerListener ← Listener ←
I/flutter ( 4259):     RawGestureDetector ← TextSelectionGestureDetector ← Semantics ← AnimatedBuilder ← _RawMouseRegion
I/flutter ( 4259):     ← MouseRegion ← IgnorePointer ← ⋯
I/flutter ( 4259):   parentData: <none> (can use size)
I/flutter ( 4259):   constraints: BoxConstraints(0.0<=w<=Infinity, 0.0<=h<=411.4)
I/flutter ( 4259):   size: MISSING
I/flutter ( 4259): This RenderObject had the following descendants (showing up to depth 5):
I/flutter ( 4259):     input: RenderRepaintBoundary#50518 NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259):       child: RenderRepaintBoundary#220cc NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259):         child: RenderCustomPaint#f181a NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259):           child: RenderRepaintBoundary#ff88a NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259):             child: RenderPointerListener#2020c NEEDS-LAYOUT NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259):     helperError: RenderConstrainedBox#98fc6 NEEDS-LAYOUT NEEDS-PAINT
I/flutter ( 4259):     container: RenderCustomPaint#39a52 NEEDS-LAYOUT NEEDS-PAINT
I/flutter ( 4259): ════════════════════════════════════════════════════════════════════════════════════════════════════
I/flutter ( 4259): Another exception was thrown: RenderBox was not laid out: _RenderDecoration#e28b7 relayoutBoundary=up7 NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259): Another exception was thrown: RenderBox was not laid out: RenderPointerListener#129f0 relayoutBoundary=up6 NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259): Another exception was thrown: RenderBox was not laid out: RenderSemanticsAnnotations#60238 relayoutBoundary=up5 NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259): Another exception was thrown: RenderBox was not laid out: RenderMouseRegion#f26dc relayoutBoundary=up4 NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259): Another exception was thrown: RenderBox was not laid out: RenderIgnorePointer#b1917 relayoutBoundary=up3 NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259): Another exception was thrown: RenderBox was not laid out: RenderFlex#54609 relayoutBoundary=up2 NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259): Another exception was thrown: RenderBox was not laid out: RenderPadding#c6b4c relayoutBoundary=up1 NEEDS-PAINT NEEDS-COMPOSITING-BITS-UPDATE
I/flutter ( 4259): Another exception was thrown: NoSuchMethodError: The method '>' was called on null.




Well, the error message has some answers for us. It suggests either using Expanded or SizedBox widget. Using Expanded means that all fixed sized widgets within the row will first be drawn. And then the rest of the space will be occupied by the expanding widgets. A textField tries to expand on its main axis infinitely. So that’s why it was taking space for all our widgets in the row.



Stuff like the Box Model.


