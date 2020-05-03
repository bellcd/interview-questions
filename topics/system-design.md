# System Design

1. What's the difference between:
   1. vertical scaling & horizontal scaling?
      1. both options cost more $$$
         1. vertical - bigger and / or better boxes (ie, more processors / more memory)
         2. horizontal - more boxes
      2. which option is better is highly situation specific
   2. forward proxy (proxy) & reverse proxy
      1. there's always a funneling involved, the key difference is whether it's inbound or outbound traffic being funneled.
      2. Proxy (forward proxy)
         1. lots of devices on an internal network routing their **OUTGOING traffic to 1 box, 1 IP address,** that forwards those requests towards their destination
         2. schools / workplaces commonly have a proxy setup
      3. Reverse Proxy
         1. **1 box, 1 IP address, that accepts INCOMING traffic** from the internet, & distributes those requests to an internal intranet
         2. Load balancers that distribute incoming requests to many server instances are a specific type of reverse proxy
2. Explain:
   1. REST
      1. TODO: finish
      2. What does REST try to imitate?
      3. Why is REST an imperfect solution?