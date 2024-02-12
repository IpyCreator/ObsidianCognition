  

  

# 3 basic git strategies are very popular and useful, let's have a sneak peek at these strategies

  

1. Feature branching
2. Gitflow
3. Trunk Based Development

  

1. ==**Feature Branching:**==  
    This strategy develops each new feature or task in a dedicated branch, Developers create a new branch for a specific feature, work on it, and then merge it back into the main branch (often called "master" or "main") when the feature is complete. This strategy allows for parallel development, isolating changes, and easier code review. It helps maintain a clean commit history.  
    Let's take an example:-  
    Suppose we have a feature to create called Video DRM then we will create a separate branch and after getting the sign-off we will merge it to master/main.  
      
    
2. ==**Gitflow:**==  
    Gitflow is a branching model that provides a structured approach to manage branching and releasing in Git. It involves two main branches: "master" and "develop." The "master" branch represents the production-ready code, and the "develop" branch serves as an integration branch for features.  
    
    We are using this branching strategy in our PW and Neet PG Apps
    
      
    
3. ==**Trunk-Based Development:**==  
    Trunk-Based Development (TBD) is a strategy that promotes a simple and streamlined branching approach. In this strategy, there is typically a single branch (e.g., "master" or "main") representing the mainline of development. Developers commit their changes directly to this branch, avoiding long-lived feature branches. Short-lived feature toggles or feature flags may be used to isolate unfinished work. TBD is suitable for fast-paced, small teams or projects focusing on continuous integration and rapid deployment.  
    

  

  

We will enhance our workflow using ==**GitFlow**==**,** currently, we are having our neetPG-Master branch that is serving the purpose of ==**develop**== branch.  
We will also add git hooks to slack for informing ios-devs that following changes are done to develop and master branches. So that every dev will take the pull and being well informed for the changes.  
  

==With our enhance workflow we will be using the following branches==

1. ==master : Protected branch==
2. ==develop : protected branch==
3. ==feature branches for every new feature==
4. ==hotfix==

  

  

==**master :**==

This will be our protected and production-ready branch, we will use tags for every release pointed to this branch commits. Only develop and hotfixes are able to merge back to ==master== branch

Whenever there is an issue in production code and we are working on ==hotfix==, once we get the sign-off for ==hotfix== we will merge it to master and develop.  
  
Following consideration must be made when working with  
==master== branch

1. Branch must be stable and always contains production-ready code, no regression bug or untested code should be present.
2. Don't add direct commits to ==master== although we will make this branch protected but avoid wasting time on such activity
3. Always use your feature branches and develop branches for adding changes through ==PR's== and ==MR's.==
4. Review of code through PR and MR's are a must, no code should go to master without review of code.
5. If possible we will use CI/CD for better deployments, Plan is to use Fastlane in the coming time.
6. We will tag the version to a specific commi tin master when our code is deployed to production  
      
      
    ==**develop**==

This is our main ongoing active branch where we will be adding our features once we get the sign-off from the QA for the feature branches.

Suppose a number of pods are working on different features and they are ready for QA, So the 1st step would be feature testing from the feature branch, once we get the QA sign-off we will merge our feature branch to develop branch.  
Once all feature branches are merged (after getting the QA Sign-off) into  
==develop== we will start the regression testing from the develop branch and will also check all features whether they are breaking something or working as expected.  
Our main production build will be triggered from  
==master== after ==develop== is merged into it.

  

==Following consideration must be made when working with develop branch==

1. ==Only add stable features that are QA signed off, no incomplete feature should be present in develop branch==
2. ==We will make this branch protected branch and avoid pushing directly to this branch, always use PR's and MR's for this branch==
3. ==Always pull the latest changes from develop branch before working on new features, and make a habit of syncing your code with develop branch==
4. ==regularly update your code with develop branch==
5. ==If possible add test cases in your code and once they are successful only then add your code to develop==
6. ==Changes to develop will always take forward with code reviews and approvals==
7. ==feature branches should be short lived, long feature branches lead to conflicts and complexity in reviews, So add short-lived features to develop==
8. ==Your branches should be very clean with incorporating commit rules==
9. ==Always communicate and make transparency when facing confusion in merging your changes because others don't know about your changes and leads to merging conflicts and deletion of others' code==
10. ==Avoid force push to your branches because that will lead to asymmetric changes in the history of develop branch  
      
    ==  
      
    ==**feature**==

Whenever we start working on any new feature we will create a branch from develop branch, all features will go to this branch. Once we finish working on the feature will give our changes for Qa sign-off. Once we get the QA sign off we will create our PR for emerging into the develop branch. We will work on reviews if we get any.

if we have a big feature and multiple devs are working on a single feature we will create a main feature branch and then others will create from that branch, Others devs who are working on small features of the main feature can provide their build for testing there features and once all features are completed they can create a merge build of all feature and merge there code to the main feature branch. Then only we will raise our PR to develop the branch.

  

==Following consideration must be made when working with feature branches==

1. ==Always create new feature branches when working on a new feature==
2. ==Use names of feature branches that are descriptive and serve the purpose.==
3. ==Always create a feature branch from develop==
4. ==update your feature branch regularly==
5. ==Changes should be focused and small==
6. ==Commit messages should be logical and descriptive, a clear commit message helps in understanding the reason for the commit==
7. ==Push your code remotely==
8. ==Communicate to fellow devs if multiple devs are working on the same feature==
9. ==Review the code of others who are working on the same feature before merging==

  
  

==**BRANCH NAMES**==

1. ==Names should be self-explanatory==
2. ==Use descriptive names==
3. ==Low case letter branches: Git is case-sensitive==
4. ==Use hyphens to separate words  
    test/solution-last  
    mahapack/ui-revamp  
    feature/drm-cdn  
    ==
5. ==Names should be concise  
    test/solution-not-working-revamp-fix  
    ==
6. ==Use prefixes to designate different branches with different purposes  
    Following are the commonly used prefixes  
    1. feature  
    2. bugfix  
    3. hotfix  
    4. release  
    5. refactor  
    ==
7. ==Dont use generic words in branch names and remove special characters==
8. ==Use the Ticket number and Issue name in your branch name  
    feature/TAP-102  
    bugfix/PRD-235  
    refactor/MAP-856  
    ==

  
  
  

==**COMMIT**==

  
A commit should contain the following rules, they are not a predefined set of rules but the industry uses them as a best practice to follow for git  

1. ==**Subject**==  
    The subject line of a commit message summarizes the essence of the change. It's typically written in the imperative mood and should be concise and descriptive  
      
      
    

```Swift
Add feature XYZ
Fix issue with ABC
Update documentation for DEF
```

## Subject Line Standard Terminology

|   |   |
|---|---|
|First Word|Meaning|
|Add|Create a capability e.g. feature, test, dependency.|
|Cut|Remove a capability e.g. feature, test, dependency.|
|Fix|Fix an issue e.g. bug, typo, accident, misstatement.|
|Bump|Increase the version of something e.g. dependency.|
|Make|Change the build process, or tooling, or infra.|
|Start|Begin doing something; e.g. create a feature flag.|
|Stop|End doing something; e.g. remove a feature flag.|
|Refactor|A code change that MUST be just a refactoring.|
|Reformat|Refactor of formatting, e.g. omit whitespace.|
|Optimize|Refactor of performance, e.g. speed up code.|
|Document|Refactor of documentation, e.g. help files.|

Subject lines must never contain (and/or start with) anything else. Especially not something that's unique to your system, like

  

- [bug] ...
- (release) ...
- \#12345 ...
- jira://...
- docs: ...

  

  

2. ==**Body**==

  
The body of a commit message provides additional context, explanations, or details about the changes made. It can help other developers understand the reasoning behind the changes and any considerations they should be aware of.  

  

Here's an example of a subject and body commit message:  
  

```Plain
Derezz the master control program: SUBJECT 

BODY:
MCP turned out to be evil and had become intent on world domination.
This commit throws Tron's disc into MCP (causing its deresolution)
and turns it back into a chess game.
```

  
3.  
==**Issue references**====:==  
  
If your project uses an issue-tracking system, you can include references to specific issues or tickets in the commit message. This helps establish a connection between code changes and the related issues  
  

```Swift
Add feature XYZ

Implements feature XYZ as requested in issue \#123
```

  
  
4.  
==**Breaking changes  
  
**==If your commit introduces breaking changes or requires special attention, you can indicate it in the commit message. This helps other developers understand the potential impact on the codebase.

  

```Swift
Fix the issue with ABC

BREAKING CHANGE: This commit modifies the public API. Update clients accordingly
```

  
  
  
==**Rules for a .gitignore file**==

  

  

1. ==**Exclude derived data**====:== Exclude the `DerivedData` directory, which contains intermediate build output and other temporary files. This directory can get quite large and is not needed for version control.

```Plain
DerivedData/
```

1. ==**Exclude user-specific data**====:== Exclude user-specific data such as user preferences, window layouts, or user-specific caches. These files are not necessary for version control and can cause conflicts when different users have different preferences.

```Plain
*.mode1v3
*.pbxuser
*.xcworkspace/xcuserdata/
```

1. ==**Exclude build output**====:== Exclude build output directories, such as the `build/` directory or`.DS_Store` files. These files can be regenerated and are not necessary for version control.

```Plain
build/
*.DS_Store
```

1. ==**Exclude pods and other dependencies**====:== Exclude dependencies installed via CocoaPods or other dependency managers, as well as their cache directories.

```Plain
Pods/
Podfile. lock
```

1. ==**Exclude local configuration files**====:== Exclude local configuration files, such as `.xcconfig` files or `.plist` files that contain configuration specific to your local environment. These files can cause conflicts when different users have different settings.

```Plain
*.xcconfig
*.xcuserdata/*.xcuserdatad/xcdebugger/
*.plist
```

1. ==**Exclude other temporary or generated files**====:== Exclude other temporary or generated files, such as `xcuserdata/` directories or `.xccheckout` files.

```Plain
xcuserdata/
*.xccheckout
```

This is not an exhaustive list and you should adjust the `.gitignore` file based on your specific project needs.

  

==**How to avoid merge conflicts in the .pbxproj file**==

  

The .pbxproj file is a configuration file used in Xcode projects, and it's prone to merge conflicts when collaborating with other developers. While it's challenging to completely avoid merge conflicts in .pbxproj files, you can follow some best practices to minimize the likelihood of conflicts and make resolving them easier. Here are some tips:

  

1. ==**Avoid simultaneous edits**====:== Coordinate with your team to avoid simultaneous edits to the .pbxproj file. If multiple developers are working on the project, communicate to ensure that only one person modifies the file at a time. This reduces the chances of conflicting changes.
2. ==**Use a version control workflow**====:== Utilize a version control system like Git to manage your project. Create feature branches for different tasks and have developers work on separate branches. This allows changes to be isolated and merged back into the main branch when they are ready.
3. ==**Regularly update your branches**====:== Keep your feature branches up to date with the latest changes from the main branch. Before merging your changes, pull the latest changes from the main branch and resolve any conflicts locally. This helps minimize conflicts when merging into the main branch.
4. ==**Avoid unnecessary reordering**====:== The .pbxproj file contains entries in a specific order. Avoid reordering the entries unless necessary, as it can increase the likelihood of conflicts. If you need to add new entries, try to maintain the existing order as much as possible.
5. ==**Be cautious with file references**====:== When adding or modifying file references in Xcode, be mindful of the paths and references in the .pbxproj file. Avoid making manual changes to the file references outside of Xcode, as it can lead to conflicts. Use Xcode's file management features to add, remove, or relocate files within your project.
6. ==**Communicate and coordinate**====:== Maintain good communication within your team about any changes or modifications you plan to make to the project. If multiple developers are working on related components or dependencies, coordinate your efforts to minimize conflicts.
7. ==**Review changes before merging**====:== Before merging a feature branch into the main branch, review the changes carefully. This includes reviewing the modifications to the .pbxproj file. This step helps catch any potential conflicts or errors before they are merged.
8. ==**Resolve conflicts promptly**====:== If conflicts do occur, address them promptly. Use a merge tool or Xcode's built-in merge conflict resolution capabilities to resolve conflicts in the .pbxproj file. Pay attention to conflicting entries, dependencies, and build settings.

  

==**Rules for creating a good PR**==

  

1. ==**Create a separate branch for each change**====:== Create a separate feature branch for each change or set of changes you want to propose. This keeps your PR focused and makes it easier to review.
2. ==**Keep your PR small and focused**====:== Keep your changes small and focused on solving a specific problem or implementing a particular feature. This makes it easier for reviewers to understand the changes and ensures that your PR doesn't become too complicated.
3. ==**Use clear and descriptive titles and descriptions**====:== Use clear and descriptive titles and descriptions for your PR to help reviewers understand what changes you are proposing and why.
4. ==**Include relevant context and documentation**====:== Include any relevant context and documentation with your PR to help reviewers understand the changes and any potential impact they may have.
5. ==**Make sure your changes build and pass tests(If test are written)**====:== Make sure your changes build and pass any relevant tests before submitting your PR. This helps ensure that your changes are ready to be reviewed and merged.
6. ==**Respond to feedback promptly**====:== Be responsive to feedback and comments from reviewers. Address any concerns or questions they have promptly and make any necessary changes to your code.
7. ==**Squash commits to keep your history clean**====:== Use `git rebase` to squash your commits into a clean and logical history before submitting your PR. This helps keep the Git history clean and makes it easier for reviewers to understand the changes you are proposing.
8. ==**Follow the team's code review process**====:== Follow the team's code review process, including any guidelines for formatting, style, and quality. This helps ensure that your code meets the team's standards and makes it easier for your changes to be merged.
9. ==**Be patient and respectful**====:== Be patient and respectful during the review process. Remember that reviewers are taking time to carefully review your changes and provide feedback to help improve the codebase.

  

  

==**Rules for solving merge conflict (We use a source tree and some of the rules are applicable when solving conflicts from the terminal/not using any merge tool )**==

1. ==**Stay calm and patient**====:== Merge conflicts can be frustrating, but it's crucial to approach them with a calm and patient mindset. Take your time to understand the conflicting changes and find the best resolution.
2. ==**Update your local branch**====:== Before attempting to resolve a merge conflict, ensure that your local branch is up to date with the latest changes from the remote repository. Use the `git pull` command to fetch and merge the latest changes.
3. ==**Review conflicting files**====:== Identify the files that have conflicts by using the `git status` command or tools such as Git GUI or GitKraken. Open the conflicting files in a text editor or a specialized merge tool to inspect the conflicting sections.
4. ==**Understand the conflicting changes**====:== Analyze the conflicting changes in each file and understand the conflicting sections. Identify the differences and consider the intended changes made by yourself and others.
5. ==**Choose the appropriate resolution strategy**====:== Decide on the resolution strategy based on the nature of the conflict and the changes involved. Git offers different options, such as manual editing, accepting one side's changes, or merging conflicting changes.
6. ==**Resolve conflicts in the affected files**====:== Open the conflicting files and manually edit them to resolve the conflicts. Locate the conflict markers (`<<<<<<<`, `=======`, and `>>>>>>>`) and modify the code to merge the conflicting changes appropriately.
7. ==**Ensure code correctness**====:== While resolving conflicts, ensure that the resulting code is correct, maintains functionality, and doesn't introduce new errors. Review the merged sections carefully and run tests to validate the changes.
8. ==**Remove conflict markers**====:== After resolving the conflicts, remove the conflict markers (`<<<<<<<`, `=======`, and `>>>>>>>`) from the affected files. These markers are only used to indicate the conflict and should not be present in the final code.
9. ==**Test your changes**====:== After resolving the conflicts, test your changes to ensure they work as intended and do not introduce any unexpected issues. Run the application, execute tests, and perform any necessary validation.
10. ==**Commit the merged changes**====:== Once you have resolved the conflicts and tested your changes, use the `git add` command to stage the resolved files. Then, create a new commit to capture the merged changes with a descriptive commit message.

  

  

==Rebasing rules==

  

Git rebase is a powerful tool used to integrate changes from one branch into another. When using `git rebase`, it's important to follow certain rules to ensure a smooth and effective rebase process. Here are some rules for using `git rebase`:

1. ==**Rebase onto a clean branch**====:== Before starting a rebase, make sure your current branch is in a clean state. Commit or stash any outstanding changes to avoid conflicts and complications during the rebase process.
2. ==**Rebase feature branches on the latest main branch**====:== If you have feature branches that need to be rebased onto the main branch, ensure that the feature branches are up to date with the latest changes in the main branch. Pull the latest changes from the main branch before initiating the rebase.
3. ==**Avoid rebasing already pushed commits**====:== Avoid rebasing commits that have already been pushed to a shared remote repository. Rewriting the commit history can cause problems for other team members who have based their work on the existing commits. Instead, consider using `git merge` for integrating changes into shared branches.
4. ==**Use interactive rebase for precise control**====:== Interactive rebase (`git rebase -i`) allows you to have precise control over the commit history. It enables you to squash, edit, reorder, or drop commits during the rebase process. Use interactive rebase when you need to clean up or organize your commit history before merging or pushing changes.
5. ==**Resolve conflicts promptly**====:== During the rebase process, conflicts may arise when Git tries to apply your changes on top of the target branch. When conflicts occur, Git will pause the rebase and indicate the conflicting sections. Resolve the conflicts by manually editing the affected files, and then continue the rebase using `git rebase --continue`.
6. ==**Test thoroughly after rebasing**====:== After completing the rebase, thoroughly test your changes to ensure that they work as expected and haven't introduced any issues. Run your application, execute tests, and perform any necessary validations before proceeding.
7. ==**Communicate with your team**====:== If you are rebasing branches that are shared among team members, communicate your intention to rebase and ensure that other team members are aware of the changes. It's important to coordinate with others to minimize conflicts and avoid confusion.
8. ==**Keep backups and use branches**====:== Before performing a rebase, consider creating a backup or a separate branch as a safety net. This allows you to revert back to the original state if something goes wrong during the rebase process.

  

**==Tools for checking source code==**

  

1. ==SwiftLint==: Enforces Swift coding style and conventions.
2. ==SwiftFormat==: Ensures consistent code formatting across your Swift project.
3. ==SonarQube==: Provides static code analysis for various languages, including Swift.
4. ==Danger==: Adds automation to code reviews and enables checks on Swift code.
5. ==SwiftMetrics==: Collects and displays metrics about your Swift code.
6. ==SwiftCop==: Enforces best practices and guidelines for clean code in Swift.
7. ==Tailor==: Cross-platform static analysis and linting tool for Swift with rule customization.
8. ==SwiftyBeaver==: Logging framework that helps detect issues and bugs in Swift code.
9. ==SwiftDoc==: Generates documentation from your Swift code, ensuring it is well-documented.
10. ==Codebeat==: Offers automated code review and analysis for Swift projects, focusing on code quality.
11. ==SourceKit-LSP==: Language Server Protocol implementation for Swift, providing code analysis and features for code editors.
12. ==Xcode Analyzer==: Built-in code analysis tool in Xcode for detecting potential issues and suggesting improvements.
13. ==XCTest==: Apple's testing framework for writing unit tests for Swift code.
14. ==Codecov==: Provides code coverage metrics for your Swift project, helping to identify untested areas.
15. ==HoundCI==: Offers automated code review and style checking for Swift projects.
16. ==SwiftCopypasta==: Detects code duplicates in your Swift project and helps you eliminate redundancy.
17. ==OCLint==: Static code analysis tool for various programming languages, including Swift.
18. ==SourceKit==: Official Swift compiler infrastructure, providing code analysis capabilities.
19. ==FauxPas==: Helps identify and fix issues related to best practices, coding standards, and performance in Swift code.
20. ==Polidor==: Analyzes Swift code for potential code smells and offers suggestions for improvement.

These tools can be integrated into our PW Git workflow and CI/CD pipelines, enabling us to ensure code quality, enforce coding standards, and identify and resolve potential issues in your Swift codebase.

  

  

  

**==Xcode features for managing source control versioning==**

  

  

1. ==Git Integration==: Xcode seamlessly integrates with Git, one of the most widely used distributed version control systems.
2. ==Repository Creation==: Xcode allows you to create Git repositories directly within the IDE.
3. ==Branching and Merging==: You can create branches, switch between them, and merge changes easily within Xcode.
4. ==Commit History==: Xcode provides a visual commit history, making it convenient to track and review changes over time.
5. ==Annotated Diffs==: Xcode displays annotated differences in code, allowing you to review changes on a line-by-line basis.
6. ==Blame Annotations==: You can view blame annotations in Xcode to see who made each change to a specific line of code.
7. ==Staging Changes==: Xcode's source control management enables you to stage-specific changes and commit them selectively.
8. ==Conflict Resolution==: Xcode provides tools to help resolve merge conflicts, making it easier to manage concurrent code changes.
9. ==Interactive Rebase==: Xcode allows you to perform interactive rebasing, helping you reorder, squash, or edit commits during the rebase process.
10. ==Tagging==: You can create tags in Xcode to mark important milestones or releases in your codebase.
11. ==Remote Repository Integration==: Xcode seamlessly integrates with remote Git repositories hosted on services like GitHub or Bitbucket.
12. ==Cloning Repositories==: Xcode enables you to clone Git repositories directly from remote sources within the IDE.
13. ==Pull and Push Operations==: Xcode supports pulling changes from remote repositories and pushing your local commits to the remote repository.
14. ==Notifications and Branch Status==: Xcode provides notifications and indicators to keep you informed about the status of branches and remote repositories.
15. ==Blame Viewer==: Xcode's blame viewer allows you to trace back the origin of each line of code, showing the author and commit details.
16. ==Commit Annotations==: You can add annotations to your commits, providing additional context or information about the changes made.
17. ==Repository Remotes==: Xcode allows you to manage multiple remotes for your Git repositories, facilitating collaboration with different teams or individuals.
18. ==File and Folder Management==: Xcode's source control management integrates with the project navigator, making it easy to add, remove, or rename files and folders while maintaining version control.
19. ==Cherry-Picking==: Xcode supports cherry-picking, enabling you to select and apply specific commits to branches without merging the entire branch.
20. ==Source Control Navigator==: Xcode's dedicated source control navigator provides an overview of the repository, showing branches, tags, and commit history.

These features of Xcode's source control management simplify collaboration, version control, and code history exploration within the IDE, enhancing the development workflow for Apple platforms.

  

  

==**Source-tree features that we can look into**==

  

  

1. ==Git and Mercurial Support==: SourceTree supports both Git and Mercurial version control systems, giving you flexibility in choosing your preferred VCS.
2. ==Intuitive Interface==: SourceTree offers a visually appealing and user-friendly interface that simplifies the management of repositories and their associated operations.
3. ==Repository Cloning==: You can easily clone remote repositories from various hosting platforms like GitHub, Bitbucket, and GitLab.
4. ==Repository Creation==: SourceTree allows you to create new repositories, whether local or remote, with just a few clicks.
5. ==Branching and Merging==: SourceTree provides seamless branching and merging capabilities, making it easy to create, switch between, and merge branches.
6. ==Visual Diff and Merge==: SourceTree offers a visual diff and merge tool that allows you to compare file differences and resolve conflicts easily.
7. ==Commit History==: You can view the commit history graphically, track changes, and explore commit details such as author, date, and message.
8. ==Staging and Discarding Changes==: SourceTree provides a convenient interface for staging specific changes and discarding unwanted modifications.
9. ==Submodule Management==: SourceTree allows you to manage Git submodules, making it easier to work with nested repositories.
10. ==Tagging and Annotating==: You can create tags and annotations in SourceTree to mark important points in your project's history.
11. ==Git Flow Support==: SourceTree offers built-in support for the Git Flow branching model, making it easier to follow the workflow and manage releases.
12. ==Push and Pull Operations==: SourceTree simplifies pushing changes to remote repositories and pulling changes from remote sources.
13. ==Interactive Rebase==: You can perform interactive rebasing within SourceTree, providing control over commit history and facilitating changesets manipulation.
14. ==Cherry-Picking==: SourceTree supports cherry-picking, enabling you to select and apply specific commits to branches without merging the entire branch.
15. ==Blame Annotations==: SourceTree provides blame annotations, allowing you to see who made each change to a specific line of code.
16. ==File Status and Change Visualization==: SourceTree visually highlights file status and changes, making it easy to identify modified, added, or deleted files.
17. ==Repository Remotes==: SourceTree allows you to manage multiple remotes for your repositories, enabling collaboration with different teams and hosting platforms.
18. ==Integrated Git LFS Support==: SourceTree seamlessly integrates with Git Large File Storage (LFS), facilitating the versioning of large binary files.
19. ==Pull Request Integration==: SourceTree integrates with popular hosting platforms like Bitbucket and GitHub, allowing you to create and manage pull requests directly within the interface.
20. ==Customizable User Preferences==: SourceTree offers a range of customizable preferences, enabling you to tailor the interface and behavior to suit your preferences and workflow.