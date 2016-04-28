Defining an operability guideline is a way to ensure that all your production
systems meet the minimum requirements to be supported within teams. Without this
guideline, different teams will have varying standards on what is required to
make a system "production" ready.

## Logging

- **Are the logs stored somewhere other than on the host itself?**

  Logs should never be stored on a single host. Instead, you should mount (and
  write to) an  external volume or have the data streamed to a centralised
  logging platform.  This becomes very benefitical if a host should die
  unexpectantly and you need to dig through the black box to determine the
  cause.

- **Are you using centralised logging?**

  Having all the logs in a single system for searching or parsing makes
  investigation and monitoring easy for all involved. If you need to jump
  between multiple logging services to gather some data, it can add overhead to
  the investigation.

- **Do you have saved search queries for common issues?**

  When starting from scratch this won't be in place however over time you should
  be able to build dashboards or save reusable queries to pull out data related
  to commonly encountered issues or data sets. This allows you to speed up the
  time to identifying the problem and not worry about small syntax issues in
  your queries.

## Monitoring

- **Is there a place where metrics (such as request per minute, response times,
  etc) are aggregated?**

  Being able to visualise changes in patterns is extremely helpful when tracking
  down when an issue started or what the impact to a particular component will
  be.

- **Do you have visual thresholds in place for your collected metrics?**

  Using visual markers in your monitoring systems allows someone with very
  little context to know where the thresholds are for a component. This can be
  in the form of a line or shaded area of the metric and can speed up incident
  response times if someone can quickly identify something has burst through a
  defined threshold and needs investigation.

## Alerting

- **Do you have automated escalation policies in place for your on call
  rotation?**

  We are all human and just because people are on call doesn't mean you get
  super powers being able to stay awake for days on end. If you support an
  application or service outside of business hours, your on call policy should
  include an automated escalation after _n_ number of calls/SMS/emails go
  unanswered. This ensures that despite a (potentially fatigued) human allowing
  an alert to go unanswered, someone else will be able to respond.

## Security

- **Are you only exposing the bare minimum that is required to operate your
  service?**

  A key to securing your infrastructure is ensuring that your attack surface is
  as small as possible. By doing this, you limit the number of potential attack
  vectors available and it gives you the oppurtunity to focus on those exposed
  surfaces.

## Automation

- **Are tasks automated where possible?**

  Whenever a task requires a human to intervene, there is a possibility that
  there will also be human error. To minimise the risk of human error, you can
  write automated scripts that a person can trigger or can be automatically
  triggered based on system events
  ([ChatOps](https://speakerdeck.com/jnewland/chatops-at-github) is a great
  example of this).

## Resiliency

- **Have you created a [resilency
  matrix](https://speakerdeck.com/sirupsen/dockercon-2015-resilient-routing-and-discovery)
  and addressed single points of failure?**

  A resiliency matrix will allow you to identify parts of your infrastructure
  that are too tightly coupled and work on ways to eliminate SPOF's and degrade
  gracefully during an outage of a single component.

- **Do you have multiple (load balanced) instances in operation?**

  Regardless of whether it is a user facing service or a database
  server, it is important to introduce at least 2 (but commonly 3) instances so
  in the event of an isolated failure, you will still have capacity to continue
  on. It's also important to ensure these instances are load balanced and health
  checks are being performed so should any of the instances return unhealthy,
  they can be ejected from the pool.

