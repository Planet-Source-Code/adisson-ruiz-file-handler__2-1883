<div align="center">

## File Handler


</div>

### Description

The class contains Static methods that allow the class user to work with a file. save, read, save as and open file dialog and some other methods. Please note that both classes are included here. FileHandler and FileFilterExtension. PLEASE RATE IT.
 
### More Info
 
<<<<<<<<<<<<    Examples    >>>>>>>>>>>>>>

String filePath = FileHandler.OpenFileDialog(this,"Open File","txt","Text files (*.txt)");

LinkedList fileContent = FileHandler.ReadFile(filePath);

ApplicationFileHeader is used to prevent users from opening files that don't belong to your application. A header is placed before the file content.

FileHandler.SaveFile(ApplicationFileHeader,fileContent ,filePath)

FileHandler.FileExists(filePath)

Linkedlists, vectors and string depending on the method invoked.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Adisson Ruiz](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/adisson-ruiz.md)
**Level**          |Advanced
**User Rating**    |4.4 (53 globes from 12 users)
**Compatibility**  |Java \(JDK 1\.1\)
**Category**       |[Files/ File Controls/ Input/ Output](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files-file-controls-input-output__2-58.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/adisson-ruiz-file-handler__2-1883/archive/master.zip)





### Source Code

```
/* Copyright: This should not be copied or edited unless with the authors permission
 * Company: <p>
 * @author: Adisson Ruiz
 * Date:  15/03/2000
 * @version 1.0
*/
/**covers most File handling needs**/
package utilities.File;
import utilities.File.FileFilterExtension;
import javax.swing.*;
import java.awt.Component;
import java.io.*;
import java.util.Vector;
import java.util.LinkedList;
public class FileHandler
{
/*****************************************************************
*   Save as FILE DIALOG BOX   *
******************************************************************/
 public static String saveAsFileDialog(Component Owner,String fileFilterExtension,String fileDescription)
 {
 return saveAsFileDialog(Owner,null,null,' ',fileFilterExtension,fileDescription);
 }
 public static String saveAsFileDialog(Component Owner,String Title,String AproveButton,char Mneumonic,String fileFilterExtension,String fileDescription)
 {
 JFileChooser chooser = new JFileChooser();
 FileFilterExtension filter = new FileFilterExtension();
 if (fileFilterExtension != null)
 {
 filter.addExtension(fileFilterExtension);
 chooser.addChoosableFileFilter(filter);
 chooser.setFileFilter(filter);
 }
 if (fileDescription != null)
 filter.setDescription(fileDescription);
 if (Title != null)
 chooser.setDialogTitle(Title);
 if (AproveButton != null)
 chooser.setApproveButtonText(AproveButton);
 if (Mneumonic != ' ')
 chooser.setApproveButtonMnemonic(Mneumonic);
 if (JFileChooser.APPROVE_OPTION == chooser.showSaveDialog(Owner))
 return chooser.getSelectedFile().getPath();
 return null;
 }
/*****************************************************************
*   OPEN FILE DIALOG BOX    *
******************************************************************/
 public static String OpenFileDialog(Component Owner,String Title)
 {
 return OpenFileDialog(Owner,Title,null,' ',null,null);
 }
 public static String OpenFileDialog(Component Owner,String Title,String Extension,String fileDescription)
 {
 return OpenFileDialog(Owner,Title,null,' ',Extension,fileDescription);
 }
 public static String OpenFileDialog(Component Owner,String Title,String AproveButton,char Mneumonic,String fileFilterExtension,String fileDescription)
 {
 JFileChooser chooser = new JFileChooser();
 FileFilterExtension filter = new FileFilterExtension();
 if (fileFilterExtension != null)
 {
 filter.addExtension(fileFilterExtension);
 chooser.addChoosableFileFilter(filter);
 chooser.setFileFilter(filter);
 }
 if (fileDescription != null)
 filter.setDescription(fileDescription);
 if (Title != null)
 chooser.setDialogTitle(Title);
 if (AproveButton != null)
 chooser.setApproveButtonText(AproveButton);
 if (Mneumonic != ' ')
 chooser.setApproveButtonMnemonic(Mneumonic);
 if (JFileChooser.APPROVE_OPTION == chooser.showOpenDialog(Owner))
 return chooser.getSelectedFile().getPath();
 return null;
 }
/*****************************************************************
*   Saves files    *
******************************************************************/
 public static boolean SaveFile(String FileHeader,Vector FileLines,String tOutputFile)
 {
 File OutputFile = new File(tOutputFile);
 FileWriter CharWriter;
 try
 {
  CharWriter = new FileWriter(OutputFile);
 }
 catch(IOException e)
 {
  return false;
 }
 if (FileLines.size()>0)
 {
	 PrintWriter LineWriter = new PrintWriter(CharWriter);
  LineWriter.println(FileHeader);
	 for (int x=0;x<FileLines.size();x++)
	  LineWriter.println(FileLines.get(x).toString());
  LineWriter.close();
	 return true;
 }
 return false;
 }
 public static boolean SaveFile(String FileHeader,LinkedList FileLines,String tOutputFile)
 {
 File OutputFile = new File(tOutputFile);
 FileWriter CharWriter;
 try
 {
  CharWriter = new FileWriter(OutputFile);
 }
 catch(IOException e)
 {
  return false;
 }
 if (FileLines.size()>0)
 {
	 PrintWriter LineWriter = new PrintWriter(CharWriter);
  LineWriter.println(FileHeader);
	 for (int x=0;x<FileLines.size();x++)
	  LineWriter.println(FileLines.get(x).toString());
  LineWriter.close();
	 return true;
 }
 return false;
 }
 public static boolean SaveFile(LinkedList FileLines,String tOutputFile)
 {
 File OutputFile = new File(tOutputFile);
 FileWriter CharWriter;
 try
 {
  CharWriter = new FileWriter(OutputFile);
 }
 catch(IOException e)
 {
  return false;
 }
 if (FileLines.size()>0)
 {
	 PrintWriter LineWriter = new PrintWriter(CharWriter);
  for (int x=0;x<FileLines.size();x++)
	  LineWriter.println(FileLines.get(x).toString());
  LineWriter.close();
	 return true;
 }
 return false;
 }
 public static boolean SaveFile(String FileLines,String tOutputFile)
 {
 File OutputFile = new File(tOutputFile);
 FileWriter CharWriter;
 try
 {
  CharWriter = new FileWriter(OutputFile);
 }
 catch(IOException e)
 {
  return false;
 }
 if (FileLines.length()>0)
 {
	 PrintWriter LineWriter = new PrintWriter(CharWriter);
  LineWriter.println(FileLines);
  LineWriter.close();
	 return true;
 }
 return false;
 }
/*****************************************************************
*   Reads files    *
******************************************************************/
 public static LinkedList ReadFile(String tInputFile)
 {
 File InputFile = new File(tInputFile);
 FileReader CharReader;
 LinkedList FileContent = new LinkedList();
 String CurrentLine;
 try
 {
  CharReader = new FileReader(InputFile);
 }
 catch(IOException e)
 {
  return null;
 }
 BufferedReader Buffer = new BufferedReader(CharReader);
 do
 {
	 try
	 {
	  CurrentLine = Buffer.readLine();
  if (CurrentLine != null)
   FileContent.add(CurrentLine);
  else
  {
   FileContent.add(null);
   Buffer.close();
  }
	 }
	 catch(IOException e)
	 {
	  return FileContent;
	 }
 }while(CurrentLine != null);
 return FileContent;
 }
 public static Vector vReadFile(String tInputFile)
 {
 File InputFile = new File(tInputFile);
 FileReader CharReader;
 Vector FileContent = new Vector(0);
 String CurrentLine;
 try
 {
  CharReader = new FileReader(InputFile);
 }
 catch(IOException e)
 {
  FileContent.add(null);
  return FileContent;
 }
 BufferedReader Buffer = new BufferedReader(CharReader);
 do
 {
	 try
	 {
	  CurrentLine = Buffer.readLine();
  if (CurrentLine != null)
   FileContent.add(CurrentLine);
  else
  {
   FileContent.add(null);
   Buffer.close();
  }
	 }
	 catch(IOException e)
	 {
	  return FileContent;
	 }
 }while(CurrentLine != null);
 return FileContent;
 }
/*****************************************************************
*  checks file for a header    *
******************************************************************/
 public static boolean CheckFileHeader(String tInputFile,String tFileHeader)
 {
 File InputFile = new File(tInputFile);
 FileReader CharReader;
 String FileHeader;
 try
 {
  CharReader = new FileReader(InputFile);
 }
 catch(IOException e)
 {
  return false;
 }
 BufferedReader Buffer = new BufferedReader(CharReader);
 try
	 {
		 FileHeader = Buffer.readLine();
  Buffer.close();
	 }
	 catch(IOException e)
	 {
  return false;
	 }
 if (FileHeader != null)
  return (FileHeader.equals(tFileHeader));
 else
  return false;
 }
/*****************************************************************
*   File exists    *
******************************************************************/
 public static boolean FileExists(String FileName)
 {
 File tFile = new File(FileName);
 return tFile.exists();
 }
}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
package utilities.File;
import javax.swing.filechooser.FileFilter;
import java.io.File;
import java.util.Hashtable;
public class FileFilterExtension extends FileFilter
{
 private String Description = "";
 private Hashtable filters = null;
 FileFilterExtension()
 {
 filters = new Hashtable();
 setDescription("Unknown File Type");
 }
 public void addExtension(String Extension)
 {
 filters.put(Extension.toLowerCase(),this);
 }
 public void setDescription(String Description)
 {
 this.Description = Description;
 }
 public String getDescription()
 {
 return Description;
 }
 public boolean accept(File file)
 {
 if (file != null)
  if (file.isDirectory())
  return true;
 String Extension = getExtension(file);
 if (Extension != null && filters.get(Extension) != null)
  return true;
 return false;
 }
 protected String getExtension(File file)
 {
 if (file != null)
 {
  String FileName = file.getName();
  int i = FileName.lastIndexOf('.');
  if (1>0 && i < FileName.length() -1)
  return FileName.substring(i+1).toLowerCase();
 }
 return null;
 }
}
```

