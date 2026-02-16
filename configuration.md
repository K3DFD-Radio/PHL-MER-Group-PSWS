## WSPRDaemon Installation and Configuration - _includes ka9q-radio_
1. Login as user _wsprdaemon_\
> **Note** This assumes you have set the user _wsprdeamon_ to not require _sudo_ per the installation instructions. If you haven't, go back and complete that step.

1. Run the following commands to create the local wsprdaemon instance:
   - $cd ~
   - $git clone https://github.com/rrobinett/wsprdaemon.git
   - $cd wsprdaemon
   - $./wsprdaemon.sh -V
> **Note:** While the wsprdaemon.git repository is _public_, git can fail to recognize this and will challenge your for a user name and password. This may fail due to password authorization being disallowed at the command line. Issue these two commands:\
         $git config --global --unset credential.helper\
         $GIT_TERMINAL_PROMPT=0 git clone https://github.com/rrobinett/wsprdaemon.git

2. In the wsprdaemon directory open the configuration file in the Nano text editor
   - $nano wsprdaemon.conf

3.
