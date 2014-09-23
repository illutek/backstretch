backstretch
===========

test project backstretch image op de body met de mogelijkheid om de afbeelding toe te voegen via een Drupal inhoudstype

Backstretch en Drupal 
 
Een site verantwoordelijke moet op een simpele manier een andere afbeelding in de achtergrond  op
de site plaatsen, deze afbeelding  wordt op zijn beurt  via de jQuery plugin backstretch, dynamische
geresized. 
De code van backstretch verwijst naar een afbeelding, zie code  
<script src="../libs/jquery/jquery.js"></script>
 <script src="../src/jquery.backstretch.js"></script>
 <script>
     $.backstretch(["afbeelding.jpg"]);  //deze regel plaatst de afbeelding in de body tag
  </script> 
Via de module File (Field) Paths https://drupal.org/project/filefield_paths kunnen we de instellingen,
in het inhoudstype ‘backgroud image’,  van het afbeeldings field uitbreiden, we geven het een vaste
bestandsnaam en  uploadmap. 

 
De mappen ‘libs’ en ‘src’ van backstretch kopiëren  en in ‘sites/all/themes/theme_naam/’ plakken. 
 

Wil je de background_editor niet teveel rechten geven, enkel de bestaande background afbeelding
kunnen aanpassen, door dat feit krijgen we een om en om situatie in de ‘background_images’ map. 
Omdat de afbeelding niet verwijdert wordt bij editeren, het ‘ background.jpg’ bestand blijft daardoor
bestaan, wordt er nu een andere afbeelding geupload dan krijgt deze de bestandsnaam
‘background_0.jpg’ 
Onderaan de page.tpl.php file volgende code plaatsen. 
<script src="<?php print base_path() . path_to_theme(); ?>/libs/jquery/jquery.js"></script>
  <script src="<?php print base_path() . path_to_theme(); ?>/src/jquery.backstretch.js"></script>
  <script>
      var base = Drupal.settings.basePath + 'sites/default/files/background_images/';
      $.ajax({
        url: base + 'background_0.jpg',
        success: function () {
          $.backstretch(base + 'background_0.jpg');
        },
        error: function () {
          $.backstretch(base + 'background.jpg');
        }
      });
  </script> 
 
Figuur 1 editor kan enkel bewerken 

 
Wordt de afbeelding verwijdert, dan wordt de code simpeler , dit omdat er enkel ‘background.jpg’
bestaat 

<script src="<?php print base_path() . path_to_theme(); ?>/libs/jquery/jquery.js"></script> 
  <script src="<?php print base_path() . path_to_theme(); ?>/src/jquery.backstretch.js"></script>
<script>
        var base = Drupal.settings.basePath + 'sites/default/files/background_images/';
         $.backstretch(base + 'background.jpg'); 
</script> 
 
 
 
