# Console Chef LWRP
## Description
Resource for console automation interaction.
LWRP is a wrapper around greenletters, https://github.com/avdi/greenletters

## Usage
The console resource is used to execute a command which expects user interaction. This resource is modelled on the chef builtin execute resource and is not similarly not idempotent. Use the <code>not\_if</code> and <code>only\_if</code> meta parameters to guard the use of this resource for idempotence.

A usage example can be found in the example recipe.

## Actions
<table>
<thead> <tr> <th>Action</th> <th>Description</th> <th>Default</th> </tr> </thead>
<tbody>
<tr> <td>run</td> <td>Default. Indicates that the command should be run.</td> <td>Yes</td> </tr>
</tbody>
</table>

## Attributes
<table>
<thead> <tr><th>Attribute</th> <th>Description</th> <th>Default Value</th></tr> </thead>
<tbody>
<tr><td>command</td><td>The name of the command to be executed.</td><td>Default value: the name of the resource block (see Syntax section above).</td></tr></td></tr>
<tr><td>creates</td><td>Indicates that a command to create a file will not be run when that file already exists.</td><td> Default value: <code>nil</code></td></tr>
<tr><td>cwd</td><td>The current working directory from which a command is run.</td><td> Default value: <code>nil</code></td></tr>
<tr><td>environment</td><td>A hash of environment variables in the form of {"VARIABLE" => "VALUE"}.</td><td> Default value: <code>nil</code></td></tr>
<tr><td>interrupts</td><td>A hash of questions/answers in the form of { regex => "answer" } that can be triggered at anytime.</td><td> Default value: <code>nil</code></td></tr>
<tr><td>answers</td><td>A hash of questions/answers in the form of { regex => "answer" } that are triggered in sequence</td></tr>
<tr><td>timeout</td><td>The amount of time (in seconds) a command will wait before timing out.</td><td> Default value: <code>3600</code></td></tr>
<tr><td>returns</td><td>The return value for a command. This may be an array of accepted values. An exception is raised when the return value(s) do not match.</td><td>  Default value: <code>0</code></td></tr>
<tr><td>provider</td><td>Optional. Use to specify a provider by using its long name. For example: provider Chef::Provider::Long::Name. See the Providers section below for the list of providers available to this resource.</td></tr>
<tr><td>user</td><td>The user name or user ID that should be changed before running a command.</td><td> Default value: <code>nil</code></td></tr>
</tbody>
</table>

## Examples
````
console "/usr/bin/adventure" do
  interrupts(
    /welcome to adventure/i => "no\n"
  )
  answers(
    /you are standing at the end of a road/i => "east\n",
    /inside a building/i => "quit\n",
    /really want to quit/i => "yes\n"
  )
end
````
Note: this example is include in the example.rb recipe.

## License and Author
Author:: [Luke Bradbury][hanskreuger] (<luke.bradbury@derby.ac.uk>)

  Copyright 2013, University of Derby

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
