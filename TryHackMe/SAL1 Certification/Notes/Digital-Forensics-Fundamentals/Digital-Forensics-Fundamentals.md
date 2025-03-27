# Digital Forensics Fundamentals
## Introduction

Forensics is referred to methods and procedures of investigation to solve crimes. Digital forensics is applied to investigate what has been declared as cyber crime. This is criminal activity conducted on or using a digital device. We use tools and techniques to investigate digital devices in a crime scene to find an analyse evidence for the corresponding legal action.

## Methodology

There are a diverse number of tools and techniques but in general, we can take the NIST model, which introduces the process in four phases:

1. **Collection:** Identify devices where you can acquire data is paramount. Let's discuss about PCs, laptops, cameras, phones, USBs, etc. In addition, ensure data is not tampered and keep an accurrate documentation.
2. **Examination:** Data needs to be filtered and the areas of interest, extracted. For example, data from a specific user from a system of an organisation.
3. **Analysis:** Analyse data, and correlate it with multiple evidence sources to draw conclusions, reconstruct the scenario based on figuring out the activities that happened.
4. **Reporting:** Report everything. It includes methodology, tools and techniques used. In addition, the report can also have recommendations. This is presented to law enforcement and executive management. Therefore, it is important to include a executive summary.

In the collection phase, there are numerous sources where you can collect evidence. Each category requires different tools and techniques. There are different types of digital forensics and some of the most common types are listed below:

* **Computer Forensics:** Investigation of computers, most commonly used in crimes.
* **Mobile Forensics:** Phones, tablets, extraction of call logs, SMS, GPS locations, discord, whatsapp.
* **Network Forensics:** Investigation of network. Network traffic logs.
* **Database Forensics:** Referred to any intrusion into DBMSs which resulted in modification and exfiltration
* **Cloud Forensics:** It is tricky due to little evidence on cloud infrastructures.
* **Email Forensics:** Phishing or any fraudulent campaigns. Email is one of the most common communication method.

## Acquiring Evidence

This is a crucial step in the DF process. You must collect it in a secure manner without tampering the original data. Methods vary on the type of device. There are some practices that must be followed and we are discussing next:

### Proper Authorisation/Consent

This is important. GET authorisation from relevant authorities. Not having approval is inadmissible in court. This is because evidence contains private and sensitive data or an idividual/organisation. 

### Chain of Custody (CoC)

This is a formal document containing all details of the evidence. Below, we have some key details lsited:

* Description (name, type).
* Name of individuals who collected it.
* Date and time of its collection.
* Storage location of each piece.
* Access times and registries of inidivuals who accessed the evidence.

This document is also to prove integrity and reliability of evidence admitted in court.

### Write Blockers

This devices makes the disk extracted from a computer for instance, to make it read-only and avoid information tampering/alteration.

## Windows Forensics

We must have in mind that one of the most common sources of evidence is a computer, most likely a personal system. They have different OSs running on it. Windows OS is a very common one that is investigated in many cases due to being part of the crime or even the victim of a crime. This secion discusses acquisition and analysis of evidence from Windows systems.

In the collection stage, we are taking images of the Windows OS. These images are "copies" in a bit-to-bit manner. There are two types of images that are taken:

* **Disk Image:** Data present from storage devices (HDD, SSD, etc). Non-volatile data.
* **Memory image:** Contains data inside the RAM memory. This is volatile data. Used to capture open files, processes, network connections, etc. This should be taken FIRST from the suspect/victim OS.

Now, some tools to discuss:

**FTK Imager:** Widely used tool to extract images of Windows computers. Has a user-friendly GUI for creating the image in various formats. It can also analyse contents of disk image. Therefore, used for both collection and analysis purposes.

**Autopsy:** Open source. Able to acquire a disk image and conduct an extensive analysis of the image, including keyword search, deleted file discovery, file metadata, extension mismatch detection, etc.

**DumpIt:** Takes a memory image from a Windows computer. It creates memory images using a CLI interface. Taken into different formats.

**Volatility:** Open-source tool to analyse memory images. Offers some useful plugins. Supports various OSs including Windows, Linux, macOS and Android.

## Practical Exercise

Everything we do on our digital devices, from smartphones to computers, leaves traces. Let’s see how we can use this in the subsequent investigation.

Our cat, Gado, has been kidnapped. The kidnapper has sent us a document with their requests in MS Word Document format. We have converted the document to PDF format and extracted the image from the MS Word file for your convenience.

You can download the attached file below to your local machine for inspection.

**Note:** For this scenario, I downloaded the content to a Ubuntu VM in VMware Workstation and rename it to *evidence.zip* as shown in the figure below:

![](/TryHackMe/SAL1%20Certification/Notes/Digital-Forensics-Fundamentals/Digital-Forensics-Exercise-Figure1.png)

When you create a text file, TXT, some metadata gets saved by the operating system, such as file creation date and last modification date. However, much information gets kept within the file’s metadata when you use a more advanced editor, such as MS Word. There are various ways to read the file metadata; you might open them within their official viewer/editor or use a suitable forensic tool. Note that exporting the file to other formats, such as `PDF`, would maintain most of the metadata of the original document, depending on the PDF writer used.

Let’s see what we can learn from the PDF file. We can try to read the metadata using the program `pdfinfo`. Pdfinfo displays various metadata related to a PDF file, such as title, subject, author, creator, and creation date. 

### Photo EXIF Data

EXIF stands for Exchangeable Image File Format, a standard for saving metadata to image files. EXIF data includes metadata embedded in image files, such as the camera model, date and time the photo was taken, GPS location, and settings like aperture or shutter speed. This information can be crucial in digital forensics to trace the origin of an image or verify its authenticity.

There are many online and offline tools to read the EXIF data from images. One command-line tool is `exiftool`. ExifTool is used to read and write metadata in various file types, such as JPEG images. If you do not have `exiftool` installed, you can install it using `sudo apt install libimage-exiftool-perl`. 

### **Answer the questions below**

1. **Using `pdfinfo`, find out the author of the attached PDF file, `ransom-letter.pdf`.** Using the command we can find that the author is *Ann Gree Sheperd*

<div align = "center">
    
![](/TryHackMe/SAL1%20Certification/Notes/Digital-Forensics-Fundamentals/Digital-Forensics-Exercise-Figure2.png)

</div>

2. **Using `exiftool` or any similar tool, try to find where the kidnappers took the image they attached to their document. What is the name of the street?** 

This command gives us loads of information like creator, profile descrption, permissons, siez, compression algorithm (in this case JPEG) and others. This question is referring to a location, perhaps filtering by GPS might give us the information we're looking for. Therefore I used the command `exiftool letter-image.jpg | grep "GPS"` and bingo, the **GPS Position** seems useful to put it on Google Maps.

![](/TryHackMe/SAL1%20Certification/Notes/Digital-Forensics-Fundamentals/Digital-Forensics-Exercise-Figure3.png)

Search for the coordinates 51°30'51.9"N 0°05'38.7"W in Google Maps and we have revealed like an alleyway in Central London between St. Paul's and Bank Stations of the Central Line London Underground. It exactly refers to Milk St. 

![](/TryHackMe/SAL1%20Certification/Notes/Digital-Forensics-Fundamentals/Digital-Forensics-Exercise-Figure4.png)

3. **What is the model name of the camera used to take this photo?**

This is another filter used in the `exiftool` tool. I used the command `exiftool letter-image.jpg | grep -i "camera"` since we are looking for the camera model and the word *"camera"* I consider it key. With that in mind, after executing the command, we find out that the Camera Model Name is a **Canon EOS R6**

![](/TryHackMe/SAL1%20Certification/Notes/Digital-Forensics-Fundamentals/Digital-Forensics-Exercise-Figure5.png)

## Conclusion

This module showed the basics of digital forensics, the multiple fields applied due to the diversity of devices and also a small lab to get engaged with some tools. In this case it was used `pdfinfo` and `exiftool` to get more information regarding the files and also valuable information such as locations, artifacts used which sounds interesting for a deeper investigation.