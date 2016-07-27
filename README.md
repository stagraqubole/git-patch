# git-patch
An iterative rebase to manage open source forks.

Open Source project forks contain custom changes. Git Patch command helps manage the commits made on a fork in a structured manner. git-patch support the following development model:
* OSS project has a master branch and tracks releases with tags or branches. 
* Forked project's development branch is a copy of a release branch or tag. 

For e.g. developers at Qubole, use the following model to develop on Facebook Presto.

PrestoDb has a master branch and tags for each release.
Qubole developers create a branch from tag `0.150` - `q-presto-0.150` which is the development branch.
All feature branches are merged to `q-presto-0.150`. 
Qubole developers want to continously test custom features on the master branch to ensure compatibility in future releases.
They created `oss-master` which is a mirror of `master` in prestodb`.
git-patch is used to manage patches and apply them on oss-master to test compatibility.

## Install
    cd ~
    git clone https://github.com/vrajat/git-patch.git
    export PATH=$PATH:~/git-patch/git-patch
    
## Initialize

    git remote add upstream <git url for upstream project>
    git fetch upstream
    git checkout upstream/master
    git checkout -b oss-master
    git init -b <development branch>
    git add .patch
    git commit -m "Add patch configuration"
    git push -u origin oss-master
    
    
## Generate patches

    git checkout oss-master
    git patch generate
    
## Apply patches


    git checkout oss-master
    git patch unclassified apply
    