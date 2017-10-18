Here at [Coolblue][coolblue], we can choose our tools from a range of technologies. A while ago, our team started moving from Microsoft MSTest to xUnit.

Although the code change was fairly simple, the build pipeline was tied with the MSTest framework, ignoring the xUnit tests. Between the requests to the deployment team to alter the team's deployment pipelines, [Nathan][nathan] challenged us to use [Cake][cakedotnet].

## What is Cake?

![The Cake][cake]
*Red Velvet cake; Photo: Jim Franco; Styling: Lydia Degaris Pursell; Original URL: http://www.myrecipes.com/recipe/red-velvet-cake-1*

Although I'm a cake monster, "Cake (C# Make) is a cross platform build automation system with a C# DSL to do things like compiling code, copy files/folders, running unit tests, compress files and build NuGet packages *([source][cakedotnet])*."

Great, this is the tool that was missing, allowing us to abstract from our CI server, speeding our development (at the end that is Agile)!

## The roller-coast

Cake allow us to build our project is many different ways with a syntax that is our bread and butter (C#). The platform is open-source, meaning that we can fix any bug, or [contribute][cake-contributing] with a module to increase the ecosystem. 

During my spare time, I started playing around with Cake in a [pet project][pullrequestsviewer]. The pet project is built using .NET Core 2.0, and the ultimate goal was to build the project in [AppVeyor][appveyor] and [TravisCI][travisci]. The build steps were:
1. Ensure the non-solution folders exists (for example, artifacts folder)
2. Clean the solution
3. Restore the NuGet packages
4. Apply the [Semantic Versioning][semver]
5. Build the solution
6. Run the tests

As a bonus it should be able to:
1. Package and push a NuGet package
2. Create and push a Docker container

Cake offers support to all these steps, either out-of-the-box feature or as a module offered by the community. 

The development was simplified since the operations to build & test my project was the same that the build server would execute. It avoids the old developer excuse "it works on my machine", ***since*** the developer machine has the same software that the build server (during the development I face this problem with AppVeyor. The solution was published [here][dotnet20-appveyor]).

## A plethora of opportunities

![Opportunities everywhere!][opportunitiesmeme]

This approach decreased the time to configure two different CI servers since it supports the executing of the scripts in Windows, Linux, and MacOS.

However, the opportunities are endless. In an enterprise environment, the software is a complex web of services and other moving parts; a team needs to be able to add a feature, testing & shipping it quickly; at the same time assuring the business that is working as expected, and more important, it doesn't introduce any regression bugs.

Using Cake, we can setup the script to deploy the necessary components on our development machines, running the tests to assure that everything works before we push our changes. This level of automation and abstraction also enables the developers to focus on delivering value (coding a new feature), rather than spending time configuring and deploying (manually) all the components to run the tests. Raise your hand who was in this situation. Yeah, every developer. :wink: 

## The final result

After a few hours around the script, both AppVeyor and TravisCI can execute it, predictably, as I do in my development environment. You can view a sample of the build logs [here][appveyorbuildlogs] and [here][traviscibuildlogs]. 

Within our team, we start to move towards this direction. All the new projects are bootstrapped with a basic Cake script (Clean, Restore, Build, Test and Create NuGet package), but the team iteratively adapts it to our development needs. In the end, a development team should be proud of the software delivered, because it improves the business, but also the team was able to use the time is an effective way.

## And for other languages/frameworks?

The same concept exists in other languages/frameworks. As short list we can:
- [CMake][cmake]
- [Gradle][gradle]
- [Fake][fake]
- [PSake][psake]
- [Rake][rake]

Be aware that is a *short list*. Out there exists other build platforms that allow you to abstract from your CI server.

[coolblue]: https://www.coolblue.nl
[nathan]: https://nathanjohnstone.wordpress.com/
[cakedotnet]: https://cakebuild.net/
[cake]: https://cdn-image.myrecipes.com/sites/default/files/red-velvet-cake-coconut-cream-cheese-frosting-crop-sl.jpg
[cake-contributing]: https://cakebuild.net/docs/contributing/contribution-guidelines
[pullrequestsviewer]: https://github.com/joaoasrosa/pullrequests-viewer
[appveyor]: https://www.appveyor.com/
[travisci]: https://travis-ci.org/
[semver]: http://semver.org/
[dotnet20-appveyor]: https://anotherlookontech.wordpress.com/2017/08/10/build-a-net-core-2-0-application-in-appveyor/
[opportunitiesmeme]: https://media.makeameme.org/created/OPPORTUNITIES-OPPORTUNITIES-EVERYWHERE-1keuus.jpg
[appveyorbuildlogs]: https://ci.appveyor.com/project/joaoasrosa/pullrequests-viewer 
[traviscibuildlogs]: https://travis-ci.org/joaoasrosa/pullrequests-viewer
[cmake]: https://cmake.org/
[gradle]: https://gradle.org/
[fake]: https://fake.build/
[psake]: https://github.com/psake/psake
[rake]: https://ruby.github.io/rake/