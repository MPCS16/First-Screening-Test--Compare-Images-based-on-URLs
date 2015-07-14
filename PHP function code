//HTML body code
<!DOCTYPE html>
<html>
<head>
  <meta charset=utf-8 />
  <link rel="stylesheet" type="text/css" media="screen" href="css/master.css" />
  <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>
  <!--[if IE]>
    <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
  <![endif]-->
  <script>
    $(document).ready(function(){
      var firstClick = true;
      $('#testC,#test').click(function(){
        $('#testC,#test').fadeOut(500);
      })
        $("#examples img").click(function(){
          if(firstClick){
            firstClick = false;
            $("#i1").val(siteURL + $(this).attr('src'));
           
          }else{
            firstClick = true;
             $("#i2").val(siteURL + $(this).attr('src'));
          }
          
          
        });
    })
    </script>
</head>
<body>

  <div id="container">
    <div id="content">
     
        <h2>Try it!</h2> 
        <div id="testC"><div id="test"><img src="http://cdn.playbuzz.com/cdn/dfbf574f-e2e4-4a07-8cc4-470ca161d6f2/adac5da9-6485-4d6d-b0fd-ebf26e38e285.jpg"><img src="http://www.explosion.com/wp-content/uploads/2014/12/813.jpg"><hr>The two image gave us this number: 0 | This means they are not similar.</div></div>        <form method="post" action="">
          <input type="text" placeholder="Image 1" name="i1" id="i1" /><input type="text" placeholder="Image 2" name="i2" id="i2" /> <input type="submit" name="submit" value="Test it" />
        </form>
       //PHP CODE FOR IMAGE COMPARISON
      <?php
class compareImages
{
	private function mimeType($i)
	{
		$mime = getimagesize($i);
		$return = array($mime[0],$mime[1]);
      
		switch ($mime['mime'])
		{
			case 'image/jpeg':
				$return[] = 'jpg';
				return $return;
			case 'image/png':
				$return[] = 'png';
				return $return;
			default:
				return false;
		}
	}  
    
	private function createImage($i)
	{
		$mime = $this->mimeType($i);
      
		if($mime[2] == 'jpg')
		{
			return imagecreatefromjpeg ($i);
		} 
		else if ($mime[2] == 'png') 
		{
			return imagecreatefrompng ($i);
		} 
		else 
		{
			return false; 
		} 
	}
    
	private function resizeImage($i,$source)
	{
		$mime = $this->mimeType($source);
      
		$t = imagecreatetruecolor(8, 8);
		
		$source = $this->createImage($source);
		
		imagecopyresized($t, $source, 0, 0, 0, 0, 8, 8, $mime[0], $mime[1]);
		
		return $t;
	}
    
    	private function colorMeanValue($i)
	{
		$colorList = array();
		$colorSum = 0;
		for($a = 0;$a<8;$a++)
		{
		
			for($b = 0;$b<8;$b++)
			{
			
				$rgb = imagecolorat($i, $a, $b);
				$colorList[] = $rgb & 0xFF;
				$colorSum += $rgb & 0xFF;
				
			}
			
		}
		
		return array($colorSum/64,$colorList);
	}
    
    	private function bits($colorMean)
	{
		$bits = array();
		 
		foreach($colorMean[1] as $color){$bits[]= ($color>=$colorMean[0])?1:0;}
 
		return $bits;
 
	}
	
    	public function compare($a,$b)
	{
		$i1 = $this->createImage($a);
		$i2 = $this->createImage($b);
		
		if(!$i1 || !$i2){return false;}
		
		$i1 = $this->resizeImage($i1,$a);
		$i2 = $this->resizeImage($i2,$b);
		
		imagefilter($i1, IMG_FILTER_GRAYSCALE);
		imagefilter($i2, IMG_FILTER_GRAYSCALE);
		
		$colorMean1 = $this->colorMeanValue($i1);
		$colorMean2 = $this->colorMeanValue($i2);
		
		$bits1 = $this->bits($colorMean1);
		$bits2 = $this->bits($colorMean2);
		
		$hammeringDistance = 100;
		
		for($a = 0;$a<64;$a++)
		{
		
			if($bits1[$a] != $bits2[$a])
			{
				$hammeringDistance--;
			}
			
		}
		  
		return $hammeringDistance;
	}
}
?>
</body>
</html>
