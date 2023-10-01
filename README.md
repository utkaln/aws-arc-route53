# aws-arc-route53
- Reference Document - [AWS Blog](https://aws.amazon.com/blogs/networking-and-content-delivery/rapidly-recover-from-application-failures-in-a-single-az/)

## Components of ARC
1. Clusters - Data plane of endpoints in five AWS regions
2. Control Panels
3. Routing Controls - logic to reroute traffice individually or in batches
4. Routing Control Health Checks
5. Safety Rules - Prevent unintentional recovery automation side effects. [AWS Documentation](https://docs.aws.amazon.com/r53recovery/latest/dg/routing-control.safety-rules.html)

#### Routing Control
- Redirects traffic by using health checks in Route 53 that are configured with DNS records associated with top level resource cells. Example - Elastic Load Balancing. Hence for Routing control to work there must be DNS endpoint
- Turn Routing Control state from `ON -> OFF` to stop traffice flow to one cell and `OFF -> ON` to send traffic flow to another cell
- This state change is driven by Route 53 health check, so routing control themselves are not health checks
- Once Routing control changes the state, then it updates the Route 53 health check to notify of the traffic flow change
- To update routing control state, api call to cluster end point must be made to try each endpoint in rotation, incase one of the cluster endpoint is not available
- 
