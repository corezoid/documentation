# Importing and exporting Corezoid objects


## Export

You can export Corezoid objects into **`json`** file.

**To export an object from Corezoid you need to:**

1. Select it and press **Download** button.
2. Press **to file** in the notification of a successful unloading
3. Select folder and save file

![](../img/create/export_object.gif)

A file with the name of the format **object_111111_1519247559.json**, where:
* `object` - object type **folder**, **conv** (process or state diagram), **dashboard**
* `111111` - object ID
* `1519247559` - unload time (unix timestamp)

will appear on your computer in the specified folder.

![](../img/create/email_export.png)

> If the process has links to other processes, you must export the folder that contains the files.

## Import

To import an object to Corezoid you need to: 

1. Click the **Create** button.
2. Select **From file** option from the drop-down list.
    ![import](../img/create/from_file.png)
3. Select **json** file with Corezoid object on your device.

The selected object will be imported to Corezoid and will appear at the current Workspace's directory.

