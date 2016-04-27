Defining an operability guideline is a way to ensure that all your production
systems meet the minimum requirements to be supported within teams. Without this
guideline, different teams will have varying standards on what is required to
make a system "production" ready.

# Table of Contents

1. [Logging](#logging)
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

