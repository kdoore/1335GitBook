#TextButton 

###TextButton Class Definition


```java

class TextButton extends Button{
  
  String label;
  
  TextButton(float _x, float _y, float _w, float _h, String _label){
    super(_x, _y, _w, _h);
    label = _label;
  }
  
  
  void display(){
    super.display();
    textSize(20);
    fill(0);
    textAlign(CENTER,CENTER);
    text(label,x+(w/2),y+(h/2));
  }
  
}  //end TextButton
  
  

```