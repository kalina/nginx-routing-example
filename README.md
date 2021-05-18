# nginx-routing-example

Creates Docker containers for external code and sets up nginx to route between them.  Cleans up when finished.

## Usage

sudo ./code/bin/multi-dev (assuming it has execute permissions)
sudo bash code/bin/multi-dev

## Postmortem

Please include a postmortem of your project with your submission. We want to
know generally how you felt about the project, anything you may have learned,
and any comments you have for interviewers. In addition, please briefly answer
the following questions.

- Did you consider approaches other than the one you chose? If you considered
  others, what tradeoffs were there to evaluate?

  I considered just starting and routing to the applications but wanted the 
  to avoid touching the so I just made containers from what should be 
  comapatible application runtimes.

- Could this be extended to support fully offline development? How?
  If the docker images have been created then this could work on a VM or laptop.  
  The host header could be set as part of the nginx config as well.

- What would you need to extend your solution with HTTPS support on port 443?
  Feel free to assume a valid TLS cert for `wistia.io` can be securely provided
  to you and any other developer.
  I'd configure the Nginx locations to use a ssl listener using the provided cert.

- Imagine other engineers on different teams caught wind of your groundbreaking
  `multi-dev` work and now want similar setups for themselves. How would you
  extend your solution to add support for other development apps? Similarly, how
  straightforward would it be to add new routes for existing supported apps,
  e.g. to have the `/publish` prefix or the subdomain `api.wistia.io` route to
  the `events-api` backend?

  With this solution, creating a new container and nginx route is pretty straightforward.
  For each app, it would take a new route in the nginx config, a Dockerfile for the app,
  and the glue in multdev to build and start the container.

- Suppose you completed this work and once Mary tried to start using it that she
  ran into a problem due to some aspect of her computer or her workflow which is
  unspecified in the list above. What are a few problems you could foresee? How
  could `multi-dev` break?
  A change in directory structures would cause problems.  
  It's cleanup is based on traps so it's somewhat brittle but it should clean up 
  from most terminations.  Another issue is if anything else tries to run on port
  80 but that would not be unique to this solution.
  
## Expectations

You are encouraged to ask any questions along the way that you would ask if you
were building this project on a team here at Wistia.

This project is not timed, so you can take as long as you need. To respect your
time, we've tried to tune the project so it can be completed in 3 hours or less
under ideal circumstances. If you find yourself getting stuck on setup or
otherwise spending time on a tangent, let us know!

We evaluate submissions on several factors, including:

- Compliance to the project requirements above
- Whether we can get the code running ourselves
- Simplicity of design and ease of use
- Clarity of communication and intent
- Mindfulness of failure modes
- Awareness of choices made and tradeoffs involved

There is no _single_ correct solution that we're looking for. We are interested
as much in how you communicate and collaborate as we are in your engineering
skills!
