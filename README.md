# gpr-publish-409

If you clone this repository, you should also change line `group = 'com.github.amkartashov'` to another group in file [lib/build.gradle](lib/build.gradle) because otherwise GitHub won't allow you to publish with 422.

To reproduce, you need to install gradle, then export your PAT credentials and start publishing in a loop:

```
hengroen:~/g/a/gpr-publish-409$ export USERNAME=amkartashov TOKEN=REDUCTED # PAT with write packages permission

hengroen:~/g/a/gpr-publish-409$ for i in {1..1000}; do gradle publish || break; done
> Task :lib:publishGprPublicationToGitHubPackagesRepository FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':lib:publishGprPublicationToGitHubPackagesRepository'.
> Failed to publish publication 'gpr' to repository 'GitHubPackages'
   > Could not PUT 'https://maven.pkg.github.com/amkartashov/gpr-publish-409/com/github/amkartashov/lib/test-20220629231048/lib-test-20220629231048.jar.sha1'. Received status code 409 from server: Conflict

* Try:
> Run with --stacktrace option to get the stack trace.
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 1s
5 actionable tasks: 4 executed, 1 up-to-date
```

