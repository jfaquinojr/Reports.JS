# stimulsoft-reports-js
Stimulsoft Reports.JS is a reporting tool for Node.js



Stimulsoft Reports.JS is a powerfull report engine for JavaScript. It can be used in any JavaScript application on client and work as node.js module on server side.

Stimulsoft Reports.JS is a part of the Stimulsoft Reports platform. Reports created in our other products will work in Stimulsoft Reports.JS and vice versa.

Get more information about Stimulsoft software at [stimulsoft.com](http://www.stimulsoft.com)



## Install

```sh
$ npm install stimulsoft-reports-js
```


## Trial Limitation

This is a trial version of Stimulsoft.Reports.JS for Node.JS. The free trial versions of Stimulsoft Reports are fully functional and will work for an unlimited time. The only limitation is a DEMO watermark displayed on each report page.



## Usage

This code allow you load report and save rendered report to file (use npm to install requred modules):
```sh
$ npm install strip-bom
$ npm install opentype.js
```

Type into your script:
```js
// File System module
var fs = require('fs');

// Remove BOM mark module
var stripBom = require('strip-bom');

// Opentype Fonts
var opentype = require('opentype.js');

// Stimulsoft Reports module
var Stimulsoft = require('stimulsoft-reports-js').Stimulsoft;
console.log("Stimulsoft Reports loaded");

//Initialize NodeJs functions
Stimulsoft.System.NodeJs.initialize();

// Load font for text drawing
var font = opentype.loadSync('node_modules/stimulsoft-reports-js/demo-files/Roboto-Black.ttf');
Stimulsoft.Base.StiFontCollection.addOpentypeFont(font);
console.log("Font loaded");

// Creating new report
var report = new Stimulsoft.Report.StiReport();
console.log("New report created");

// Loading report template
var reportTemplate = fs.readFileSync('node_modules/stimulsoft-reports-js/demo-files/SimpleList.mrt', "utf8");
report.load(reportTemplate);
console.log("Report template loaded");

// Loading demo data
var demoData = stripBom(fs.readFileSync('node_modules/stimulsoft-reports-js/demo-files/Demo.json', "utf8"));
report.dictionary.databases.clear();
report.regData("Demo", "Demo", demoData);
console.log("Demo data loaded into the report. Tables count: ", report.dataStore.count);

// Renreding report
report.render();
console.log("Report rendered. Pages count: ", report.renderedPages.count);

// Saving rendered report to file
var renderedReport = report.saveDocumentToJsonString();
fs.writeFileSync('./SimpleList.mdc', renderedReport);
```

For saving report to HTML format add this code:
```js
// Creating export settings
var settings = new Stimulsoft.Report.Export.StiHtmlExportSettings();

// Creating export service
var service = new Stimulsoft.Report.Export.StiHtmlExportService();

// Creating text writer 
var textWriter = new Stimulsoft.System.IO.TextWriter();

// Creating HTML writer
var htmlTextWriter = new Stimulsoft.Report.Export.StiHtmlTextWriter(textWriter);

// Exportong report into HTML writer
service.exportTo(report, htmlTextWriter, settings);

// Set HTML-data to string
var resultHtml = textWriter.getStringBuilder().toString();

// Saving string with rendered report in HTML into a file
fs.writeFileSync('./SimpleList.html', resultHtml);
console.log("Rendered report saved into HTML-file.");
```

Export to PDF require using this code:
```js
// Creating export settings
var settings = new Stimulsoft.Report.Export.StiPdfExportSettings();

// Creating export service
var service = new Stimulsoft.Report.Export.StiPdfExportService();

// Creating MemoryStream
var stream = new Stimulsoft.System.IO.MemoryStream();

// Exportong report into the MemoryStream
service.exportTo(report, stream, settings);

// Converting MemoryStream into Array
var data = stream.toArray();

// Converting Array into buffer
var buffer = new Buffer(data, "utf-8")

// Saving rendered report in PDF into a file
fs.writeFileSync('./SimpleList.pdf', buffer);
console.log("Rendered report saved into PDF-file.");
```



## License

STIMULSOFT, STIMULSOFT REPORTS
DEVELOPER LICENSE AGREEMENT FOR STIMULSOFT SOFTWARE

This Stimulsoft, ("STIMULSOFT") Developer License Agreement ("DLA") is a legal agreement between you, software developer ("DEVELOPER") and STIMULSOFT for STIMULSOFT REPORTS identified above and including components, source code (if provided), demos, intermediate files, media, printed materials, and "online" or electronic documentation ("SOFTWARE") contained in this installation file.

STIMULSOFT grants to you, a personal, nonexclusive license to install and use the SOFTWARE for the sole purposes of designing, developing, testing, and deploying application programs which you create. If you are an entity, you must designate one individual within your organization to use the SOFTWARE in the manner provided herein.

The SOFTWARE is runtime royalty-free for Redistributables.

By installing, copying, or otherwise using the SOFTWARE, you agree to be bound by the terms of this DLA. If you do not agree to any part of the terms of this DLA, DO NOT INSTALL, USE, DISTRIBUTE IN ANY MANNER, OR REPLICATE IN ANY MANNER, ANY PART, FILE OR PORTION OF THE SOFTWARE.

All SOFTWARE is licensed, not sold.

The demonstration version includes the following restriction - on all pages the inscription "Demo" is deduced. The full version of a product does not contain these restrictions. It is necessary for you to be registered before use the full version of a product. You can use the demonstration version of a product with an unlimited period of time.

RIGHTS
You may install and use one copy of the SOFTWARE, including any and all source code if provided, or any prior version legally licensed for the same operating system, on a single computer. Developer may make two additional copies of the SOFTWARE: a second copy for his or her exclusive use on a portable computer and a third copy for his or her exclusive use on a home computer. You acknowledge and agree that the SOFTWARE in source code if provided form remains a confidential trade secret of STIMULSOFT.

You may transfer all of your rights to use the SOFTWARE to another person, provided that you transfer to that person all of the software and documentation provided in this package (including this license agreement), and transfer or destroy all copies in any form. Remember, once you transfer the SOFTWARE, you no longer have any right to use it, and the person to whom it is transferred may use it only in accordance with the copyright law, international treaty, and this license.

REGISTER THIS SOFTWARE; DEVELOPER LICENSE GIVES YOU THE RIGHT TO:

All the potential of a registered version become available for you;
 
Free technical support and notifications on the new versions of SOFTWARE;

Updates, upgrades (to all minor and major versions) and fixes. STIMULSOFT will provide you with free updates, upgrades (to all minor and major versions) and fixes of the SOFTWARE, within one year after you purchase it. If you are using the demonstration version of the SOFTWARE, STIMULSOFT will not provide you updates, upgrades to minor version and fixes related to the SOFTWARE. 

To register SOFTWARE read file "readme.rtf" or visit web-site http://www.stimulsoft.com.

Following registration, you may continue to use the SOFTWARE in accordance with this Agreement for an unlimited period (irrespective of whether the subscription period has lapsed) unless this Agreement is terminated in accordance with its Termination provisions.

RESTRICTIONS
You may not rent, lease, lend, copy, modify, sub-license, time-share, electronically transmit or receive the SOFTWARE, except as provided in this license, or as directed by STIMULSOFT. You may alter the source code of the SOFTWARE, excluding file names and copyright inscriptions, for the purpose of your use as authorized by this Agreement, but you may not otherwise translate, reverse engineer, decompile or disassemble or otherwise alter the SOFTWARE or its documentation.

You may not reverse engineer, decompile, create derivative works, modify, translate, or disassemble the SOFTWARE, and only to the extent that such activity is expressly permitted by applicable law notwithstanding this limitation. You agree to take all reasonable, legal and appropriate measures to prohibit the illegal dissemination of the SOFTWARE or any of its constituent parts and redistributables to the fullest extent of all applicable local, US Codes and International Laws and Treaties regarding anti-circumvention, including but not limited to, the Geneva and Berne World Intellectual Property Organization (WIPO) Diplomatic Conferences.

The DEVELOPER shall not expose SOFTWARE API to its customers, but only its own API. 

The DEVELOPER may NOT distribute the SOFTWARE, in any format, to other users for development or application compilation purposes. Specifically, if DEVELOPER creates a component using the SOFTWARE as a constituent component, DEVELOPER may NOT distribute the component created with the SOFTWARE (in any format) to users to be used at design time and or for ANY development purposes. This restriction applies to design time within IDE (Microsoft Visual Studio and others).

YOU MAY NOT CREATE ANY TOOL OR SOFTWARE THAT DIRECTLY OR INDIRECTLY COMPETES WITH THE SOFTWARE WHICH UTILIZES ALL OR ANY PORTION OF THE SOFTWARE. 

The SOFTWARE is licensed as a single PRODUCT. The SOFTWARE and its constituent parts and any provided redistributables may not be reverse engineered, decompiled, disassembled or separated for use on more than one computer, nor placed for distribution, sale, or resale as individual creations by DEVELOPER. The provision of source code, if included with the SOFTWARE, does not constitute transfer of any legal rights to such code, and resale or distribution of all or any portion of all source code and intellectual property will be prosecuted to the fullest extent of all applicable local, federal and international laws. All STIMULSOFT libraries, source code if provided, redistributables and other files remain STIMULSOFT exclusive property.  You may not distribute any files, except those that STIMULSOFT has expressly designated as Redistributable. 

SOFTWARE may include certain files ("Redistributables") intended for distribution by you to the users of programs you create. Redistributables include those files selected for deployment by an install utility provided with the SOFTWARE. In any event, the Redistributables for the SOFTWARE are only those files specifically designated as such by STIMULSOFT. Subject to all of the terms and conditions in this DLA, you may reproduce and distribute exact copies of the Redistributables, provided that such copies are made from the original copy of the SOFTWARE or the copy transferred to a single hard disk. Copies of Redistributables may only be distributed with and for the sole purpose of executing application programs permitted under this DLA that you have created using the SOFTWARE. Under no circumstances may any copies of Redistributables be distributed separately.


REDISTRIBUTABLES
The following files are considered redistributables under this DLA: 

Stimulsoft Reports.Ultimate

.net
Stimulsoft.Controls.dll
Stimulsoft.Controls.Win.dll
Stimulsoft.Base.dll
Stimulsoft.Database.dll
Stimulsoft.Database.Wpf.dll
Stimulsoft.Editor.dll
Stimulsoft.Report.dll
Stimulsoft.Report.Check.dll
Stimulsoft.Report.Win.dll
Stimulsoft.Report.Web.dll
Stimulsoft.Report.Mvc.dll
Stimulsoft.Report.WebFx.dll
Stimulsoft.Report.Wpf.dll
Stimulsoft.Report.Wpf.BlackTheme.dll
Stimulsoft.Report.Wpf.Office2003BlueTheme.dll
Stimulsoft.Report.Wpf.Office2003OliveGreenTheme.dll
Stimulsoft.Report.Wpf.Office2003SilverTheme.dll
Stimulsoft.Report.Wpf.Office2007BlackTheme.dll
Stimulsoft.Report.Wpf.Office2007BlueTheme.dll
Stimulsoft.Report.Wpf.Office2007SilverTheme.dll
Stimulsoft.Report.Wpf.Office2010BlueTheme.dll
Stimulsoft.Report.Wpf.Office2013Theme.dll
Stimulsoft.Report.Design.dll
Stimulsoft.Report.WebDesign.dll
Stimulsoft.Report.WpfDesign.dll
Stimulsoft.Report.Helper.dll
Stimulsoft.Report.DesignHelper.dll
Stimulsoft.Base.SL.dll
Stimulsoft.Controls.SL.dll
Stimulsoft.Report.SL.dll
Stimulsoft.Report.Check.SL.dll
Stimulsoft.Report.Helper.SL.dll
Stimulsoft.Report.SLDesign.dll
Stimulsoft.Report.Viewer.SL.dll
Stimulsoft.Report.WebSL.dll
Stimulsoft.Report.WebDesignSL.dll
Stimulsoft.Base.RT.dll
Stimulsoft.Controls.RT.dll
Stimulsoft.Report.RT.dll
Stimulsoft.Helper.RT.dll
Stimulsoft.Report.Viewer.RT.dll
Stimulsoft.Report.Design.RT.dll
Stimulsoft.Report.Mobile.dll
Stimulsoft.Report.MvcMobile.dll
Stimulsoft.Report.MobileDesign.dll

JS
stimulsoft.designer.js
stimulsoft.reports.js
stimulsoft.viewer.js
All css files

Java
All jar files

PHP
config.xml 
swfobject.js
playerProductInstall.swf 
designer.html
viewer.html
DesignerFx_PHP.swf
ViewerFx_PHP.swf 
index.php
handler.php
localization.php
database_xml
database_mssql.php
database_mysql.php
database_odbc.php
database_oracle.php
database_pg.php

Flex
Stimulsoft_ViewerFx.swc
Stimulsoft_DesignerFx.swc

Localization files

Stimulsoft Reports.Web
Stimulsoft.Base.dll
Stimulsoft.Report.dll
Stimulsoft.Report.Web.dll
Stimulsoft.Report.WebFx.dll
Stimulsoft.Report.Mobile.dll
Stimulsoft.Report.Mvc.dll
Stimulsoft.Report.MvcMobile.dll
Stimulsoft.Report.WebDesign.dll
Stimulsoft.Report.MobileDesign.dll
Localization files

Stimulsoft Reports.Net
Stimulsoft.Controls.dll
Stimulsoft.Controls.Win.dll
Stimulsoft.Base.dll
Stimulsoft.Database.dll
Stimulsoft.Editor.dll
Stimulsoft.Report.dll
Stimulsoft.Report.Check.dll
Stimulsoft.Report.Win.dll
Stimulsoft.Report.Design.dll
Stimulsoft.Report.Helper.dll
Stimulsoft.Report.Web.dll
Localization files 

Stimulsoft Reports.Wpf
Stimulsoft.Base.dll
Stimulsoft.Database.Wpf.dll
Stimulsoft.Report.dll
Stimulsoft.Report.Check.dll
Stimulsoft.Report.Wpf.dll
Stimulsoft.Report.Wpf.BlackTheme.dll
Stimulsoft.Report.Wpf.Office2003BlueTheme.dll
Stimulsoft.Report.Wpf.Office2003OliveGreenTheme.dll
Stimulsoft.Report.Wpf.Office2003SilverTheme.dll
Stimulsoft.Report.Wpf.Office2007BlackTheme.dll
Stimulsoft.Report.Wpf.Office2007BlueTheme.dll
Stimulsoft.Report.Wpf.Office2007SilverTheme.dll
Stimulsoft.Report.Wpf.Office2010BlueTheme.dll
Stimulsoft.Report.Wpf.Office2010WhiteTheme.dll
Stimulsoft.Report.WpfDesign.dll
Stimulsoft.Report.Helper.dll
Localization files

Stimulsoft Reports.Silverlight
Stimulsoft.Base.dll
Stimulsoft.Base.SL.dll
Stimulsoft.Controls.SL.dll
Stimulsoft.Report.dll
Stimulsoft.Report.SL.dll
Stimulsoft.Report.Check.SL.dll
Stimulsoft.Report.Helper.SL.dll
Stimulsoft.Report.SLDesign.dll
Stimulsoft.Report.Viewer.SL.dll
Stimulsoft.Report.WebSL.dll
Stimulsoft.Report.WebDesignSL.dll
Localization files

Stimulsoft Reports.WinRT
Stimulsoft.Base.RT.dll
Stimulsoft.Controls.RT.dll
Stimulsoft.Report.RT.dll
Stimulsoft.Helper.RT.dll
Stimulsoft.Report.Viewer.RT.dll
Stimulsoft.Report.Design.RT.dll
Localization files

Stimulsoft Reports.Java
All *.jar files
Localization files

Stimulsoft Reports.PHP
config.xml 
swfobject.js
playerProductInstall.swf 
designer.html
viewer.html
DesignerFx_PHP.swf
ViewerFx_PHP.swf 
index.php
handler.php
localization.php
database_xml
database_mssql.php
database_mysql.php
database_odbc.php
database_oracle.php
database_pg.php
Localization files

Stimulsoft Reports.Flex
Stimulsoft_ViewerFx.swc
Stimulsoft_DesignerFx.swc
Localization files

YOU ARE NOT AUTHORIZED TO REDISTRIBUTE ANY OTHER FILE CONTAINED IN THE SOFTWARE.


COPYRIGHT
All title and copyrights in and to the SOFTWARE (including but not limited to any images, demos, source code if provided, intermediate files, packages, photographs, distributables, animations, video, audio, music, text, and "applets" incorporated into the SOFTWARE the accompanying printed materials, and any copies of the SOFTWARE) are owned by STIMULSOFT or its subsidiaries. The SOFTWARE is protected by copyright laws and international treaty provisions. Therefore, you must treat the SOFTWARE like any other copyrighted material except that you may install the SOFTWARE on a single computer provided you keep the original solely for backup or archival purposes. You may not copy the printed materials accompanying the SOFTWARE. Therefore, you must treat the SOFTWARE like any other copyrighted material except that you may install the SOFTWARE (as stated in the Rights clause) provided you keep the original solely for backup or archival purposes.

INSTALLATION AND USE
The license granted in this DLA for you to create your own compiled programs and distributes your programs and the Redistributables (if any), is subject to all of the following conditions:
1. You may not remove or alter any STIMULSOFT copyright, trademark or other proprietary rights notice contained in any portion of STIMULSOFT libraries, source code if provided, Redistributables or other files that bear such a notice;  
2. STIMULSOFT provides no warranty at all to any person, other than the Limited Warranty provided to the original purchaser of the SOFTWARE, and you will remain solely responsible to anyone receiving your programs for support, service, upgrades, or technical or other assistance, and such recipients will have no right to contact STIMULSOFT for such services or assistance;  
3. You will indemnify and hold STIMULSOFT its related companies and its suppliers, harmless from and against any claims or liabilities arising out of the use, reproduction or distribution of your programs;
4. Your programs containing SOFTWARE must be written using a licensed, registered copy of the SOFTWARE;
5. Your programs must add primary and substantial functionality, and may not be merely a set or subset of any of the libraries, code, Redistributables or other files of the SOFTWARE;
6. You may not use STIMULSOFT's or any of its supplier's names, logos, or trademarks to market your programs.

TERMINATION
Without prejudice to any other rights or remedies, STIMULSOFT will terminate this DLA upon your failure to comply with all the terms and conditions of this DLA. In such events, you must destroy all copies of the SOFTWARE and all of its component parts including any related documentation, and must remove ANY and ALL use of such technology immediately from any applications using technology contained in the SOFTWARE developed by you, whether in native, altered or compiled state.

LIMITED WARRANTY
NO WARRANTIES. STIMULSOFT expressly disclaims any warranty for the SOFTWARE.  THE SOFTWARE AND ANY RELATED DOCUMENTATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING, WITHOUT LIMITATION, THE IMPLIED WARRANTIES OF MERCHANTABILITY, OR FITNESS FOR A PARTICULAR PURPOSE, OR NONINFRINGEMENT. THE ENTIRE RISK ARISING OUT OF USE OR PERFORMANCE OF THE SOFTWARE REMAINS WITH YOU.  To the maximum extent permitted by applicable law, in no event shall STIMULSOFT be liable for any special, incidental, indirect, or consequential damages whatsoever (including, without limitation, damages for loss of business profits, business interruption, loss of business information, or any other pecuniary loss) arising out of the use of or inability to use the SOFTWARE or the provision of or failure to provide Support Services, even if STIMULSOFT has been advised of the possibility of such damages.

SUPPORT SERVICES
STIMULSOFT may provide you with support services related to the SOFTWARE ("Support Services"). Use of Support Services is governed by the STIMULSOFT policies and programs described in the user manual, in "online" documentation and/or other STIMULSOFT-provided materials. Any supplemental SOFTWARE code provided to you as part of the Support Services shall be considered part of the SOFTWARE and subject to the terms and conditions of this DLA. With respect to technical information you provide to STIMULSOFT as part of the Support Services, STIMULSOFT may use such information for its business purposes, including for SOFTWARE support and development. STIMULSOFT will not utilize such technical information in a form that personally identifies you.

GENERAL PROVISIONS
This DLA may only be modified in writing signed by you and an authorized officer of STIMULSOFT. If any provision of this DLA is found void or unenforceable, the remainder will remain valid and enforceable according to its terms.  If any remedy provided is determined to have failed for its essential purpose, all limitations of liability and exclusions of damages set forth in the Limited Warranty shall remain in effect.

You, as the DEVELOPER, agree and ascend to the adherence to all applicable international treaties regarding copyright and intellectual property rights which shall also apply.  In addition, you, as DEVELOPER, agree that any local law(s) to the benefit and protection of STIMULSOFT ownership of, and interest in, its intellectual property and right of recovery for damages thereto will also apply. IF CONDITION OF THIS LICENSE DISAGREES WITH LOCAL LAW(S), THAN YOU CAN NOT USE SOFTWARE.

MISCELLANEOUS
STIMULSOFT reserves all rights in the SOFTWARE not specifically granted in this DLA.

This license is subject to change without notice in future updates to the SOFTWARE.

YOU ACKNOWLEDGE THAT YOU HAVE READ THIS AGREEMENT, UNDERSTAND IT AND AGREE TO BE BOUND BY ITS TERMS AND CONDITIONS. YOU FURTHER AGREE THAT IT IS THE COMPLETE AND EXCLUSIVE STATEMENT OF THE AGREEMENT BETWEEN US, WHICH SUPERSEDES ANY PROPOSAL OR PRIOR AGREEMENT, ORAL OR WRITTEN, AND ANY OTHER COMMUNICATIONS BETWEEN US RELATING TO THE SUBJECT MATTER OF THIS AGREEMENT.

Copyright (C) 2003-2015 Stimulsoft, All rights reserved.
