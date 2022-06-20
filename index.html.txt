<!DOCTYPE html>
<html>
   <head>
      <title>Test dijit programmatic layout</title>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
      <style type="text/css">
         @import "dojo/resources/dojo.css";
         @import "dijit/themes/claro/document.css";
         @import "dijit/themes/claro/claro.css";
         @import "dgrid/css/dgrid.css";
         @import "dgrid/css/skins/claro.css";
         html, body {
            padding: 0;
            margin: 0;
            width: 100%;
            height: 100%;
            overflow:hidden;
         }
         .dijitBorderContainer .dgrid {
            height: 100%;
         }
      </style>
      <script type="text/javascript">
         var dojoConfig = {
            async : true,
            parseOnLoad : true
         }
      </script>
      <script type="text/javascript" src="dojo/dojo.js"></script>
      <script type="text/javascript">
         require(["dojo/ready", "dojo/parser", "dojo/dom-construct", "test/TopBC"], function(ready, parser, domConstruct, BC){
            ready(function(){
               var pBC = new BC({}, "bc");
               pBC.startup();
            });
         });
      </script>
   </head>
   <body class="claro">
      <div id="bc"></div>
   </body>
</html>
