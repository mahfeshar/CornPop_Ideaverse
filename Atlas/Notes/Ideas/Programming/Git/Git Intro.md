---
up:
  - "[[Git - GitHub MOC]]"
related: 
created: 2024-06-24
---


Git is a popular version control system. It was created by Linus Torvalds in 2005, and has been maintained by Junio Hamano since then.
It is used for: (==Version Control System== VCS)
- Tracking code changes to source code
- Recovers older versions
- Tracking who made changes
- Coding collaboration

![[Pasted image 20240624063153.png]]

- Free and open-source software under GNU or General  Public License
- Distributed Version Control System (DVCS): Easy accessibility of project copies.

### Basic terms
![[SSH]]

- Repository المستودع: Contains project folders.
- Fork: Copy of a repository.
  
- Pull Request: To request for review and approval.
- Working directory: Contains files and subdirectories on your computer that are associated with a Git repository
- Commit: a snapshot of the project's current state at a specific point in time ==with a description of the changes made==
- Branch فرع: Separate line of development that allows you to work on features or fixes independently 
- Merge: Combines changes from one branch to another
- Clone نسخة: creates a local copy of the remote Git repository

#### What's Fork?
لما حد من برا بيطلب انه يغير حاجة بيعمل حاجة اسمها fork ولو بدأ يغير حاجة مبيعرفش يرفع على ال repo بس ممكن يعمل request واما يتقبل او لا

لو عايز تدخل ال repo وتبقا عضو فيه لازم المسئول يضيفك من الموقع نفسه

settings ⇒ collaborators
### What does Git do?
- Manage projects with **Repositories**
- **Clone** a project to work on a local copy
- Control and track changes with **Staging** and **Committing** [[Git Staging Environment]]
- **Branch** and **Merge** to allow for work on different parts and versions of a project [[Git Branch]]
- **Pull** the latest version of the project to a local copy
- **Push** local updates to the main project

### Working with Git
- Initialize Git on a folder, making it a **Repository** [[Git Getting started#Initialize Git]]
- Git now creates a hidden folder to keep track of changes in that folder
- When a file is changed, added or deleted, it is considered **modified**
- You select the modified files you want to **Stage**
- The **Staged** files are **Committed**, which prompts Git to store a **permanent** snapshot of the files
- Git allows you to see the full history of every commit.
- You can revert back to any previous commit.
- Git does not store a separate copy of every file in every commit, but keeps track of changes made in each commit!

you can know all about commands at [[Git help]]
### What is GitHub?
- Git is not the same as GitHub.
- GitHub makes tools that use Git.
- GitHub is the largest host of source code in the world, and has been owned by Microsoft since 2018.

You will have a big problem with [[Git User name and password]]