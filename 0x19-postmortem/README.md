## Postmortem: BooktifuL Requests Failure Incident

## Issue Summary:
Duration: June 10, 2023, 06:00 - June 10, 2023, 19:20 (WAT)
Impact: Outage on an isolated Ubuntu 14.04 container running an Apache web server
Root Cause: Typo in the file name within the WordPress application, leading to a critical error and server unavailability

## Timeline:

    Issue Detected: June 15, 2023, 12:00 (WAT)
    Detection Method: Gloria, the assigned bug debugger, noticed the issue upon opening the System Engineering & DevOps project.
    Actions Taken:
        Checked running processes using ps aux and confirmed the Apache web server processes were active.
        Explored the sites-available folder in the /etc/apache2/ directory and identified the serving location of the web server as /var/www/html/.
        Ran strace on the root and www-data Apache processes to trace system calls.
        Discovered an -1 ENOENT (No such file or directory) error related to the file /var/www/html/wp-includes/class-wp-locale.phpp when analyzing the www-data process with strace.
        Located the erroneous .phpp file extension in the wp-settings.php file, specifically on line 137, which attempted to include the file class-wp-locale.phpp.
        Rectified the typo by removing the trailing p from the file name.
        Conducted a successful test using curl to verify the server's functionality.
        Created a Puppet manifest, 0-strace_is_your_friend.pp, to automate the error fix in case of similar incidents.

## Root Cause and Resolution:
The root cause of the outage was identified as a typographical error within the WordPress application. Specifically, in the wp-settings.php file, the inclusion of the file class-wp-locale.phpp resulted in a critical error. The correct file name, located in the wp-content directory, should have been class-wp-locale.php.

To resolve the issue, the typo was corrected by removing the trailing p from the file name. This simple fix restored the functionality of the server, and subsequent tests confirmed its proper operation. Additionally, a Puppet manifest, 0-strace_is_your_friend.pp(https://github.com/Ogoobaby/alx-system_engineering-devops/blob/master/0x17-web_stack_debugging_3/0-strace_is_your_friend.pp), was created to automate the correction process in case of future occurrences of this error.

## Corrective and Preventative Measures:
To prevent similar outages in the future, the following measures are recommended:

*    Thoroughly test applications before deployment to catch potential errors, such as typos or critical bugs, at an early stage.
*    Implement status monitoring services, like UptimeRobot, to promptly alert system administrators about any website outages or performance issues.
*    Regularly review and validate the codebase to ensure there are no such critical errors that can disrupt the application's functionality.

## Tasks to Address the Issue:

*    Review and update the testing process to include rigorous checks for typographical errors or critical bugs.
*    Implement a status monitoring service to promptly detect and report any future outages or performance degradation.
*    Conduct regular code reviews and validations to identify and address potential critical errors or inconsistencies in the application.
*    Maintain an updated and comprehensive documentation repository to assist developers and debugging teams in addressing similar issues efficiently.

## Conclusion:
The BooktifuL Requests Failure Incident was caused by a typographical error within the WordPress application. The incorrect file name, class-wp-locale.phpp, led to a critical error and subsequent server unavailability. By identifying and rectifying the typo, the system.
