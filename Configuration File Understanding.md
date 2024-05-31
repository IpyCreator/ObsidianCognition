

### Step-by-Step Explanation:

1. **Require Libraries**:
   - `xcodeproj`: Used to manipulate Xcode project files.
   - `gitlab`: Used to interact with the GitLab API.
   - `fileutils`: Provides methods to work with the file system.
   - `open3`: Allows running shell commands and capturing their output.

2. **Define a Configuration DSL**:
   - `ConfigDSL` class: Allows defining a configuration using a Ruby DSL (Domain Specific Language). It stores the configuration in a hash.
   - `configure` method: Evaluates a block in the context of `ConfigDSL` and returns the configuration hash.

3. **Fetch GitLab Repositories**:
   - `fetch_gitlab_repos` method: Configures the GitLab client and fetches repositories from a specified group.

4. **Parse Command-Line Arguments**:
   - `parse_arguments` method: Retrieves command-line arguments for the app version, certificates, provisioning profile, and targets. Returns a hash of these values.

5. **Create Xcode Project Structure**:
   - `create_xcode_project` method: Uses `xcodeproj` to create an Xcode project with the specified targets. Each target is configured with an example file (`AppDelegate.swift`).

6. **Add Git Submodules**:
   - `add_git_submodules` method: Adds the specified git submodules to the project using shell commands.

7. **Install CocoaPods**:
   - `install_pods` method: Installs pods if a Podfile is provided and exists.

8. **Main Script Execution**:
   - Reads configuration, fetches GitLab repositories, creates the Xcode project, adds submodules, and installs pods. Prints a success message with the app version.

### Making Command-Line Arguments Optional

To make the command-line arguments optional, we can provide default values if they are not supplied. Here's the updated script:

```ruby
require 'xcodeproj'
require 'gitlab'
require 'fileutils'
require 'open3'

# Define the DSL for configuration
class ConfigDSL
  def initialize(&block)
    @config = {}
    instance_eval(&block)
  end

  def method_missing(name, *args)
    @config[name] = args.size > 1 ? args : args.first
  end

  def to_h
    @config
  end
end

def configure(&block)
  ConfigDSL.new(&block).to_h
end

# Fetch GitLab repositories
def fetch_gitlab_repos(token, group)
  Gitlab.endpoint = 'https://gitlab.com/api/v4'
  Gitlab.private_token = token
  Gitlab.group_repositories(group)
end

# Parse arguments, providing default values if not supplied
def parse_arguments
  {
    app_version: ARGV[0] || '1.0.0',
    certificates: ARGV[1] || 'default_certificates',
    provisioning_profile: ARGV[2] || 'default_provisioning_profile',
    targets: ARGV[3..-1].empty? ? ['default_target'] : ARGV[3..-1]
  }
end

# Create Xcode project structure
def create_xcode_project(project_name, targets)
  project = Xcodeproj::Project.new("#{project_name}.xcodeproj")
  
  targets.each do |target_name|
    target = project.new_target(:application, target_name, :ios, '9.0')
    group = project.main_group.new_group(target_name)
    group.new_file('AppDelegate.swift') # Example file
  end
  
  project.save
end

# Add git submodules to the project
def add_git_submodules(submodules)
  submodules.each do |submodule|
    Open3.capture3("git submodule add #{submodule}")
  end
end

# Install pods if Podfile is provided
def install_pods(podfile_path)
  if File.exist?(podfile_path)
    Open3.capture3("pod install")
  end
end

# Main script execution
if __FILE__ == $0
  config = configure do
    gitlab_token 'YOUR_GITLAB_TOKEN'
    gitlab_group 'your-group-name'
    project_name 'MyXcodeProject'
    submodules ['https://github.com/your/submodule1.git', 'https://github.com/your/submodule2.git']
    podfile_path 'Podfile'
  end

  args = parse_arguments
  repos = fetch_gitlab_repos(config[:gitlab_token], config[:gitlab_group])

  create_xcode_project(config[:project_name], args[:targets])
  add_git_submodules(config[:submodules])
  install_pods(config[:podfile_path])

  puts "Xcode project created successfully with version #{args[:app_version]}"
end
```

### Explanation of Changes:

1. **Updated `parse_arguments` Method**:
   - Provides default values for `app_version`, `certificates`, `provisioning_profile`, and `targets` if they are not supplied as command-line arguments.
   - If no targets are supplied, it defaults to `['default_target']`.

2. **Ensuring Optional Command-Line Arguments**:
   - The script will run with or without command-line arguments, using defaults if necessary.

You can now run the script without any arguments, and it will use the provided default values:

```sh
ruby setup_project.rb
```

Or you can supply some or all arguments as needed:

```sh
ruby setup_project.rb 2.0.0 custom_certificates custom_provisioning_profile custom_target1 custom_target2
```

This makes the script more flexible and user-friendly.