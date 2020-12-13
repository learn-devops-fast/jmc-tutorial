The main performance difference in the method profiling is that MC/JFR uses sampling, and only samples a few threads per sampling interval. It uses a similar approach to AsyncGetCallTrace (see for example http://psy-lob-saw.blogspot.com/2016/06/the-pros-and-cons-of-agct.html)

Since I work with MC/JFR, I'm not as familiar with how VisualVM does it's sampling profiling, but I believe it's not using the same method.

MC/JFR has it's data gathering engine deeply integrated into the HotSpot JVM, VisualVM uses external APIs/MXBeans. This also helps JFR to lower the performance overhead. Generally, JFR is designed to find the hot spots, rather than gathering data that 100% correct but might slow your application down and affect the actual behavior. This goes for both the method and allocation sampling, as well as other information about latency events (wait/sleep/block), where only the events above a certain threshold are recorded. I'm less familiar with how this compares for VisualVM.

Other than that, the two tools have different feature sets, none of which is a superset of the other.
