## Support for password authentication was removed on August 13, 2021

#

Example:

    remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
    remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.
    fatal: Authentication failed for 'https://github.com/siddiquinoor/devtools.git/'

### Solution

- Step - 01: Login to your Github account.
- Step - 02: Click on the profile icon on the top right corner.
- Step - 03: Click on "Settings".
- Step - 04: Click on "<> Developer Settings" menu on the bottom left corner.
- Step - 05: Click on "Personal access tokens" from the left side.
- Step - 06: Click on "Generate new token".
- Step - 07: Enter an Note and then by selecting options click on "Generate token".

Finally copy the token and use it as a password in your command line when it prompts for Password.
