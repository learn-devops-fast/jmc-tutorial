Creating a Recording Using Triggers
You can use the Console in Java Mission Control to set triggers. A trigger is a rule that executes an action whenever a condition specified by the rule is true. For example, you can create a rule that triggers a flight recording to commence whenever the heap size exceeds 100 MB. Triggers in Java Mission Control can use any property exposed through a JMX MBean as the input to the rule. They can launch many other actions than just Flight Recorder dumps.

Define triggers on the Triggers tab of the JMX Console. For more information on how to create triggers, see the Java Mission Control help.
