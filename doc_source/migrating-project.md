# Migrating Your Project<a name="migrating-project"></a>

Lumberyard 1\.5 introduces application descriptor files, which list all modules used by a project\. Each project requires two application descriptor files in its asset directory:
+ `dev/project_asset_directory/Config/Game.xml`
+ `dev/<project_asset_directory/Config/Editor.xml`

Create these files by running the `Bin64\lmbr.exe projects populate-appdescriptors` command from the command line\.

If you change gems using the Project Configurator, Lumberyard automatically updates the application descriptor files\. If you manually edit a project's `gems.json` file, however, you must update these files by running the `Bin64\lmbr.exe projects populate-appdescriptors` command from the command line\.