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
### Subprocess with shell equals true - CWE-20 Improper Input Validations
Two files were flagged for this security patter: release.py and security config.py.

* release.py (lines 308 and 309)
  * This file is not called at runtime, and is a utility for promoting code to release. Additionally, this warning only becomes applicable 'if appropriate care is not taken to sanitizize any user provided or variable input'; both highlighted lines are used to run git commands to retrieve information about the contributors of the project, and neither take user input, but hard coded git commands that have been found to be safe.
* tests/kafkatest/services/security/security_config.py (line 83)
  * This file is run during tests, and is used to configure security during the test. The line in question never takes user input, but does take variable input. After reviewing all calls to this function, we found that all variable values are hard coded, and do not need sanitization.

### Hardcoded temp directory
Three files were flagged for this security pattern: kafka.py, security_config.py, and delegation_token_test.py.

* None of the flagged files are called at runtime, but are used during set up for tests. The files assume the temporary directory is located at /tmp, and have hardcoded that value in several variables. Typically Apache Kafka is run in a Linux environment, but it is possible to run in other environments. Although none of these files are called at runtime, it would better practice to use the following library to check the location of the temporary directory:

```python
import tempfile

tmp = tempfile.gettempdir()
```
### Prohibit unencrypted sockets - CWE-311 Missing Encryption of Sensitive Data
Four files were flagged for this security patter: DynamicConnectionQuotaTest.scala, SocketServerTest.scala, EdgeCaseRequestTest.scala, and ZkFourLetterWords.scala.

At first glance, this flag seems to be a serious problem, but after review we have found several reasons why these are false positives.
* None of these files are called at runtime, and are only called during tests.
* All of the files that have been flagged for this error level issue utilize the unencrypted sockets in question for traffic on localhost only, and do not transmit data over-the-wire.

### Prohibit weak random - CWE-330 Use of Insufficiently Random Values
19 potential issues for this pattern were discovered. Codacy's description of the pattern is as follows:

>The use of a predictable random value can lead to vulnerabilities when used in certain security critical contexts. For example, when the value is used as:
>* a CSRF token
>* a password reset token (sent by email)
>* any other secret value
>* A quick fix could be to replace the use of java.util.Random with something stronger, such as java.security.SecureRandom.

This is closely related to [CWE-330: Use of Insufficiently Random Values](https://cwe.mitre.org/data/definitions/330.html) where "the software may use insufficiently random numbers or values in a security context that depends on unpredictable numbers."

For manual review, I went through each of the potential issues to determine if they were using a predictable random number generator in one of the security critical contexts mentioned above.

* core/src/main/scala/kafka/log/LogConfig.scala, core/src/main/scala/kafka/security/authorizer/AclAuthorizer.scala, core/src/main/scala/kafka/utils/Throttler.scala
	* These files use a random number to vary the length of time processes are delayed. For example, in AclAuthorizer.scala if an update to the access control list fails, the client is put to sleep for a brief amount of time so that it isn't competing with other clients also trying to update the list. The random number adds jitter to vary the length of time these clients are sleeping, so that multiple competing clients aren't all asleep at the same time. Because this is not one of the security critical contexts mentioned earlier, using a predictable random number in this situation isn't a concern.
* core/src/main/scala/kafka/tools/ConsoleConsumer.scala
	* This file uses a random number to give a consumer group a unique identifier. Again, this isn't a security critical context, so it's fine to use a predictable random number in this situation.

The remaining flagged files are located in a test folder and aren't called at runtime.

### Subprocess without shell equals true - CWE-20 Improper Input Validations
Two files were flagged for this issue: release.py and kafka-merge-pr.py.

This issue is similar to the 'Subprocess popen with shell equals true' above in which care should be taken to validate user input and sanitize variables, and in that case both files were not called at runtime and did not take user input. Similarly, neither of the files flagged for this issue are called at runtime, but are utility scripts used for promoting and merging code, and neither take user input.

### Prevent path traversal - CWE-22 Improper Limitation of a Pathname to a Restricted Directory ("Path Traversal")
Two files were flagged for this issue: Log.scala and LogManager.scala.

This issue takes into consideration that the 'path traversal attack technique allows an attacker access to files, directories, and commands that potentially reside outside the web document.' After review, we have found that neither of the flagged files poses a risk, as both are related to internal logging. The methods that were flagged are used to perform basic CRUD operations on files related to internal logs, and are not exposed to the user.

## Collaboration
The team efficiently divided the project code for manual review and subsequent analysis via Codacy.  The tickets were created and appropriately migrated through the stages of completion, with review.  However, we had some difficulty concerning how to classify the security issues, which we resolved as a team by agreeing to investigate issues within hotspot categories.  We will carry the same decision-making structure to the final part of the project.

### [Pull Requests](https://github.com/isxbot/software-assurance/pulls?q=is%3Apr+is%3Aclosed)

### [Project Board](https://github.com/isxbot/software-assurance/projects/3)

