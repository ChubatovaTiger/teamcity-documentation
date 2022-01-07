[//]: # (title: Super User Access)
[//]: # (auxiliary-id: Super User Access;Super User)

The _Super User_ login mode allows accessing the server UI with System Administrator permissions. For example, if the administrator forgot the credentials or needs to fix authentication-related settings. The login is performed using an authentication token that can be found in the server logs.

A Super User token is also used to access the server maintenance pages displayed on the server start when a manual action is required to proceed with the server startup.

The authentication token is automatically generated on every server start. The token is printed in the server console and [`teamcity-server.log`](teamcity-server-logs.md) under the `TeamCity\logs` directory (search for the "Super user authentication token" text). The line is printed on the server start and on any login page submit without a username specified.

To log in as a Super User, use an empty username and the authentication token as the password on the login page.

A Super User is not a usual TeamCity user and does not have any personal settings, such as __Changes__ page and Profile section (that is there is no way to receive notifications). The Super User has all [System Administrator permissions](managing-roles-and-permissions.md).

Any number of Super Users can log in to TeamCity simultaneously without affecting each other's sessions.

Instead of using an empty username, you can also go to the `<TeamCity_server_URL>/login.html?super=1` page and enter the Super User authentication token. On loading the Super User login page, the Super User token is printed into the server log and console again for your convenience.

The Super User login is enabled by default, but it can be disabled by specifying the `teamcity.superUser.disable=true` [internal property](server-startup-properties.md#TeamCity+Internal+Properties).

<seealso>
        <category ref="concepts">
            <a href="guest-user.md">Guest User</a>
        </category>
</seealso>
