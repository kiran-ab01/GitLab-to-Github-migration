# GitLab-to-Github-migration
Gitlab to github migration

git clone --bare <gitlab clone url>

git clone --bare --branch <branch-name> <gitlab clone url>(will clone the repository in a bare format and only fetch the branch <branch-name>)

git push -- mirror <github clone url>

--------------------------------------------------------------------------------------------------------------------------------------------

gitlab to github migration(lfs track)

download bfg cleaner -- https://rtyley.github.io/bfg-repo-cleaner/

execute the below command (copy the bfg cleaner downloaded jar file path along with file name and include the extension file to lfs track and mention gitlab repo name)

java -jar <path to>bfg-x.x.x.jar --convert-to-git-lfs "*.{png,mp4}" --no-blob-protection <repo-name>.git 

cd <repo-name>.git

git reflog expire --expire=now --all && git gc --prune=now --aggressive

git lfs install

git push -- mirror <github clone url>

---------------------------------------------------------------------------------------------------------------------------------------------------------

Step 1: Bare clone the repository

git clone --bare repository-link


Step 2: Install git LFS

git lfs install

Step 3: Get the large files details in the repository

git lfs migrate info --everything

Step 4: Convert all the large files with extensions found from above command to LFS on all the branch in repository

git lfs migrate import --include="*.war,*.sql" --everything

git lfs migrate import --include="*.java,*.jar,*.pdf,*.zip,*.xml" --everything


Step 5: Run GC on repository

git reflog expire --expire=now --all

--git reflog expire --expire=now --all --dry-run(to test the command without actually removing any entries)

git gc --aggressive --prune=now (ill perform a full cleanup of the repository, removing unreachable objects, compacting the object database, pruning the reflog, and deleting expired tags)

--git gc --aggressive --prune=now --dry-run (will print a list of all of the objects that would be removed if the command were not run with the --dry-run option)


Step 6: Force push the repository

git push --mirror --force REPO_URL(--force option can be dangerous, as it can overwrite any existing branches or tags on the remote repository)

git push --mirror --force --tags REPO_URL

------------------------------------------------------------------------------------------------------------------------------------------
Remove war/jar file and push repo

1. java -jar bfg-1.14.0.jar --delete-files ECapexServ.war --no-blob-protection ecapexServer.git
2. 
3. cd ecapexServer.git
4. 
5. git reflog expire --expire=now --all && git gc --prune=now --aggressive
6. 
7. git push command

