# Analysis — RTT vs. Speed-of-Light

## Q1 Which city has the highest inefficiency ratio?

Frankfurt had the highest inefficiency ratio in my results at 3.99, with 
London close behind at 3.86. I expected Lagos to be the worst since it's 
in Africa extremely far away, but it actually came in at 2.75. The reason 
Frankfurt and London score so high is most likely because we're using 
HTTP requests, not raw pings. Google is probably routing our HTTP traffic 
through load balancers and CDN infrastructure that adds overhead. Almost 
every city returned RTTs between 200-240ms regardless of how far away it 
was, which tells me Google's network is doing a lot of work behind the 
scenes that inflates our numbers.

## Q2 Which city is closest to the theoretical minimum?

Sydney had the lowest ratio at 1.41, which was suprising because it's the 
furthest city at 16240 km away. My best explanation is that Google has a 
strong local presence in Sydney, so the HTTP request probably got handled 
by a nearby server rather than traveling the full distance. This actually 
made me realize that HTTP-based measurement has a limitation. CDN caching 
can make a far city look more efficient than a closer one, which isn't 
really measuring the network path, it's measuring where Google decided to 
answer from.

## Q3 Why does Africa route through Europe?

From what I can tell, it comes down to where the undersea cables were 
built and why. Most of the major cables were laid in the 1990s and 2000s 
when the big markets were North America, Europe, and Asia. Africa didn't 
have enough traffic volume at the time to justify building direct cables 
there, so carriers just connected Africa to Europe and backhauled the 
traffic through there.

So a packet from Boston to Lagos probably goes Boston, to London, down 
the West African coast, which is a much longer path than going straight 
across the Atlantic. That's why Lagos didn't perform as badly as I 
expected (the routing penalty is real, it's just that Google's 
infrastructure masked it in our HTTP measurement)

To actually fix this you'd need direct US to Africa submarine cables 
(Google's Equiano cable and Meta's 2Africa project are working on this), 
more local internet exchange points inside African countries so traffic 
doesn't have to leave the continent, and lower costs for accessing landing 
stations so more cable investment makes sense financially.