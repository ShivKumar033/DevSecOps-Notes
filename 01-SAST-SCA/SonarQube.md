- SonarQube is a static analysis platform or software used to continously inspect code quality and security.
**Three Components:-**
1. Code Quality Checks
	Bugs (Logic error)
	Vulnerabilities (Security issues)
	Code smell ( Maintianability Problem)
	Security Hostpots

2. Code Coverages
	- It is akey metric that measure the precentage of your source code executed by your automated tests.
3. Quality GateCheck
	- In SonarQube is a set of PASS/FAIL conditions that determine if a project is ready for developement. 
	- Like:- if code scan 80% pass the scan then depeloy

### SonarQube Architecture.

1. **SonarQube Server**
	1. UI web ( manage rules, quality profile)
	2. Computer Engine ( Processess scan resutl )
	3. Search Engine ( Index issues )
	4. Databases

2. **SonarQube Scanner**
	- Run on the developer machine or CLI
	- scan source code and send-back to the SonarQube server.