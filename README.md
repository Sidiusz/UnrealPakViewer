# UnrealPakViewer ##

Graphical tool for viewing UE4 Pak files, supports UE4 pak/ucas files

* Tree view and list view support for viewing files in pak/ucas
* Support for opening multiple pak/ucas files at the same time
* Support for searching, filtering and sorting in the list view
* Support for viewing specific content composition information of UAsset files
* Percentage display of the size of each folder, file and file type
* Support multi-threaded decompression of Pak files
* Support for loading AssetRegistry.bin resource registry

## Function ##

### Open Pak file ###

![OpenPak.png](Resources/Images/OpenPak.png)

Or drag the Pak file directly into the UnrealPakViewer window to open it, and if the Pak file is encrypted, a password entry box will pop up

![AESKey.png](Resources/Images/AESKey.png)

Enter the corresponding AES key in Base64 format to open the Pak file

### View Pak file summary information ###

![PakSummary.png](Resources/Images/PakSummary.png)

* Mount Point: Default mount point
* Pak Version: Pak file version number
* Pak File Size: Pak file size
* Pak File Count: the number of files packed in the Pak
* Pak Header Size: Pak file header size
* Pak Index Size: Pak index area size
* Pak Index Hash: Pak index area hash
* Pak Index Is Encrypted: Whether the Pak index area is encrypted or not
* Pak File Content Size: Pak file content area size
* Pak Compression Methods: The compression algorithm used for the files in Pak

### Load the resource registry ###

![LoadAssetRegistry.png](Resources/Images/LoadAssetRegistry.png)

Cook will generate a resource registry in the *Saved/Cooked/[Platform]/[Project]/Metadata/DevelopmentAssetRegistry.bin* path after completion, which contains information on resource types, reference relationships, etc., and can be loaded through the Load Asset Registry to analyze the size share information of each resource type

### File tree view ###

![TreeView.png](Resources/Images/TreeView.png)

A tree structure listing the directories and files contained in the Pak, and information about the size of the directories as a percentage of the total size

#### Select a directory to view the details of that directory on the right ####

![FolderDetail.png](Resources/Images/FolderDetail.png)

* Name: Directory name
* Path: Path of the directory
* Size: Directory size after decompression
* Compressed Size: The size of the directory after it is compressed
* Compressed Size Of Total: The ratio of compressed size of the directory to the total Pak size
* Compressed Size Of Parent: The ratio of compressed size of the directory to the parent directory
* File Count: Number of files in the directory

and information on the percentage of each file type in that directory (requires loading the AssetRegistry.bin registry)

![FolderDetailClass.png](Resources/Images/FolderDetailClass.png)

#### After selecting a file you can view the details of that file on the right ####

![FileDetail.png](Resources/Images/FileDetail.png)

Some additional information compared to the directory

* Class: the type of the file
* Offset: the starting position of the file serialized in Pak
* Compression Block Count: number of compression blocks
* Compression Block Size: Compression block size
* Compression Method: file compression algorithm
* SHA1: File hash value
* IsEncrypted: whether the file is encrypted or not

If a .uasset or .umap file is selected, you can also view the serialization information inside that file

![AssetSummary.png](Resources/Images/AssetSummary.png)

* Guid: The Guid of the resource
* bUnversioned: whether the serialization is done with the engine version information
* FileVersionUE4: File format version number
* FileVersionLicenseeUE4: File format version number (license)
* TotalHeaderSize: uasset's file header size
* PackageFlags: uasset package flags
* ImportObjects: import table information (referenced external object information)
![ImportObjects.png](Resources/Images/ImportObjects.png)
* Index: The index of the object in the imported table
* ObjectName: The name of the object
* ClassName: the type of the object
* ClassPackage: The package where the object type is located
* FullPath: The full path to the object
* ExportObjects: information about the export table (which objects are inside the resource), the serialized size of the export table is the corresponding .uexp file size, you can click SerialSize and SerialOffset columns to sort
![ExportObjects.png](Resources/Images/ExportObjects.png)
Index: Index of the object in the exported table
* ObjectName: The name of the object
* ClassName: the type of the object
* SerialSize: the serialized size of the object
* SerialOffset: Serialization offset of the object
* FullPath: The full path of the object within the package
* bIsAsset:
* bNotForClient: non-client resource
* bNotForServer: non-server resource
* TemplateObject: The object's template object
* Super: The parent object
* Dependencies: the specific object information referenced by the object, before the colon for the reference type, followed by the path to the specific object referenced
 ![ObjectDependencies.png](Resources/Images/ObjectDependencies.png)
* Serialization Before Serialization: Serialized objects to be serialized before serialization
* Create Before Serialization: Objects to be created before serialization
* Serialization Before Create: Objects to be serialized before creation
* Create Before Create: Objects to be created before creation
* Dependency packages: Resources that this resource depends on
  ![DependencyPackages.png](Resources/Images/DependencyPackages.png)
* Dependent packages: resources that depend on this resource, this is searched within the current Pak, if the package is subcontracted the results may be missing
  ![DependentPackages.png](Resources/Images/DependentPackages.png)
* Names: All FName information associated with this resource
  ![Names.png](Resources/Images/Names.png)

#### right-click menu ####

![TreeViewContext.png](Resources/Images/TreeViewContext.png)

Right-clicking on a directory or file will bring up a right-click menu with the following functions

* Extract: Decompress the selected directory or file.
* Export To Json: Export the selected directory or file information to a Json file.
* Export To Json: Export the selected directory or file information to a Csv file.
* Show In File View: If a file is selected, jump to the corresponding position of the file in the file list

### File list view ###

![ListView.png](Resources/Images/ListView.png)

The file list view displays information about files in Pak in a table format, with support for sorting by clicking on column headings

#### Type filter ####

![ClassFilter.png](Resources/Images/ClassFilter.png)

Filter the files in the list by type

#### Filename filter ####

![NameFilter.png](Resources/Images/NameFilter.png)

Filter the files in the list by file name

#### right-click menu ####

![ListViewContext.png](Resources/Images/ListViewContext.png)

Right-click on the selected file to bring up the context menu with the following functions

* Extract: Decompress the selected file.
* Export To Json: Export the information of the selected file to a Json file.
* Export To Json: Export the information of the selected file to a Csv file.
* Show In Tree View: If a single file is selected, it will jump to the tree view
* Copy Columns: Copies the corresponding column information to the clipboard
* View Column: Hide/Show Columns
* Show All Columns: Displays all columns

## Compile ##

Clone the code to the *Engine\Source\Programs* directory and regenerate the solution to compile it

* Compiled version of the engine
  * 4.24
  * 4.25
  * 4.26
  * 4.27
  * 4.28

## TODO ##

* commandline application
* Pak compare visiualize
* resource preview
* resource load heat map
