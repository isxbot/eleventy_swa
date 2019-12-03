# Static Code Analysis

## Review Strategy
Because Apache Kafka has a large code base, we want to focus our review efforts on security related issues. To do this we have developed the following code review strategy:
* Perform static code analysis using Codacy.
* Perform manual code review on identified hotspots.

## Static Code Analysis Results [![Codacy Badge](https://api.codacy.com/project/badge/Grade/7d7ae59298434e099ba793a26e5b5c8d)](https://www.codacy.com/manual/isxbot/kafka?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=isxbot/kafka&amp;utm_campaign=Badge_Grade)

**Summary of Key Findings from Codacy**
* Total Issues: 9091
* Categories:
  * Security: 186
  * Error Prone: 2990
  * Code Style: 5903
  * Performance: 12

While the total number of issues is 9091, only 186 are related to security issues, and of those issues one is info level, 181 are warning level, and 4 are error level.

The code scan also indicated that there are six security pattern hotspots:
* Subprocess popen with shell equals true
* Hardcoded tmp directory
* Prohibit unencrypted sockets
* Prohibit weak random
* Subprocess without shell equals true
* Prevent path traversal

## Manual Code Review
