#### GIT installation/Version check 
git --version 
Sample output: git version 2.17.1.windows.2

_GIT is distributed version control system_. So the code repository is located in both local system and also on remote server like github. GIT 

#### Initialize local git repository
git init

#### Adding files to indexing area of git
git add .   
  or 
git add *

Once the files are added to the indexing only then git looks for its status like added/modified/deleted, etc.

#### Remote repository verbose (fetch and pull url)
git remote -v
Please understand that we can have more than 1 remote repository to fetch or push the repository to.

#### Clone remote github repository
git clone <github_remote_url>

