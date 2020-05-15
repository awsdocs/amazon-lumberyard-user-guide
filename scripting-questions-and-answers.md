# Scripting in Amazon Lumberyard: Questions and Answers<a name="scripting-questions-and-answers"></a>

See the following questions and answers for automating gameplay using Script Canvas and Lua\.

** Q\. My studio requires visual scripting\. What are the best practices that we should use? **  
A\. See [Script Canvas Best Practices](https://docs.aws.amazon.com/lumberyard/latest/userguide/script-canvas-best-practices.html)\.

** Q\. What's the future of visual scripting? **  
A\. The game industry has used visual scripting successfully to increase iteration speed, streamline workflows, reduce production costs, and ship large scale AAA games\. Lumberyard's goal for Script Canvas is to continue to make it easier to use so that game developers can reduce their iteration time and achieve their goals more efficiently\.

** Q\. When should I convert a Lua script to C\+\+ to improve performance? **  
A\. When a script can be identified as performing poorly and faster algorithms are not available, consider converting the script to C\+\+\.

** Q\. How can I profile my Lua memory and CPU usage? **  
A\. We recommend using the RAD Telemetry Gem\. The `lumberyard_version\dev\Gems\RADTelemetry\Code\Include\RADTelemetry\ProfileTelemetry.h file` provides a RAD Telemetry specific implementation of the `AZ_PROFILE_FUNCTION`, `AZ_PROFILE_SCOPE`, and `AZ_PROFILE_SCOPE_DYNAMIC` performance instrumentation markers\.  
For more information, see [RAD Telemetry Gem](https://docs.aws.amazon.com/lumberyard/latest/userguide/gems-system-gem-rad-telemetry.html)\.