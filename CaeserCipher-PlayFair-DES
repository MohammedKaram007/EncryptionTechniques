/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package securityapp;
import java.net.URL;
import java.util.ArrayList;
import java.util.ResourceBundle;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.fxml.FXML;
import javafx.fxml.Initializable;
import javafx.scene.control.Button;
import javafx.scene.control.ComboBox;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.input.MouseEvent;
/**
 *
 * @author KaRaM
 */
public class FXMLDocumentController implements Initializable {
    @FXML
    private TextField plainTxt;
    @FXML
    private TextField keyTxt;
    @FXML
    private TextField cipherTxt;
    @FXML
    private Button encBtn;
    @FXML
    private Button decBtn;
    @FXML
    private Button rstBtn;
    @FXML
    private ComboBox<String> TechMenu;
    @FXML
    private Label check;
    
    String ALPHABET = "abcdefghijklmnopqrstuvwxyz";
    String prevRight,prevLeft,newRight,newLeft,newSubkey;
    byte [] shiftingTimes = {1,1,2,2,2,2,2,2,1,2,2,2,2,2,2,1};
    ArrayList <String> subKeys = new ArrayList<>();
    byte [] permutedChoice1 = {57,49,41,33,25,17,9,1,58,50,42,34,26,18,10,2,59,51,43,35,27,19,11,3,60,52,44,36,63,55,47,39,31,23,15,7,62,54,46,38,30,22,14,6,61,53,45,37,29,21,13,5,28,2,12,4};
    byte [] permutedChoice2 = {14,17,11,24,1,5,3,28,15,6,21,10,23,19,12,4,26,8,16,7,27,20,13,2,41,52,31,37,47,55,30,40,51,45,33,48,44,49,39,56,34,53,46,42,50,36,29,32};
    byte [] initialPermutation = {58,50,42,34,26,18,10,2,60,52,44,36,28,20,12,4,62,54,46,38,30,22,14,6,64,56,48,40,32,24,16,8,57,49,41,33,25,17,9,1,59,51,43,35,27,19,11,3,61,53,45,37,29,21,13,5,63,55,47,39,31,23,15,7};
    byte [] finalPermutation = {40,8,48,16,56,24,64,32,39,7,47,15,55,23,63,31,38,6,46,14,54,22,62,30,37,5,45,13,53,21,61,29,36,4,44,12,52,20,60,28,35,3,43,11,51,19,59,27,34,2,42,10,50,18,58,26,33,1,41,9,49,17,57,25};
    byte [] functionPermutation = new byte [56];
    @Override
    public void initialize(URL url, ResourceBundle rb) {
        EventHandler <MouseEvent> eventhandler = (MouseEvent event) -> {
        String choice=  TechMenu.getSelectionModel().getSelectedItem();
        if (choice.equalsIgnoreCase("Caesar"))
        CaesarEnc();
        else if(choice.equalsIgnoreCase("PlayFair"))
        PlayFairEnc();
        else if(choice.equalsIgnoreCase("DES"))
        check.setText(rotateLeft(plainTxt.getText(), 3)); //rotateLeft(plainTxt.getText(), 3);
        };
        encBtn.addEventHandler(MouseEvent.MOUSE_CLICKED, eventhandler);
    
        EventHandler <MouseEvent> eventhandler2 = (MouseEvent event2) -> {
        String choice=  TechMenu.getSelectionModel().getSelectedItem();
        if (choice.equalsIgnoreCase("Caesar"))
        CaesarDec();
        else if(choice.equalsIgnoreCase("PlayFair"))
        PlayFairDec();
        else if(choice.equalsIgnoreCase("DES"))
        check.setText(rotateLeft(plainTxt.getText(), 3)); //rotateLeft(plainTxt.getText(), 3);
        };
        decBtn.addEventHandler(MouseEvent.MOUSE_CLICKED, eventhandler2);
        
        EventHandler <MouseEvent> eventhandler3 = (MouseEvent event3) -> {
        plainTxt.setText("");
        cipherTxt.setText("");
        keyTxt.setText("");
        };
        rstBtn.addEventHandler(MouseEvent.MOUSE_CLICKED, eventhandler3);
    }
    private void CaesarEnc() {        
        String PlainText;
        PlainText = plainTxt.getText().toLowerCase();
        String cipherText = "";
        int key = Integer.parseInt(keyTxt.getText()); 
        for (int i = 0; i < PlainText.length(); i++)
        {
            int index = ALPHABET.indexOf(PlainText.charAt(i));
            int newIndex = (index + key) % 26;
            char newChar = ALPHABET.charAt(newIndex);
            cipherText += newChar;
        }
        cipherTxt.setText(cipherText);
    }
    private void CaesarDec() {
     String CipherText = cipherTxt.getText().toLowerCase();
     String plainText = "";
        for (int i = 0; i < CipherText.length(); i++)
        {
            int key = Integer.parseInt(keyTxt.getText());
            int index = ALPHABET.indexOf(CipherText.charAt(i));
            int newIndex = (index - key) % 26;
            if (newIndex < 0)
                newIndex = ALPHABET.length() + newIndex;
            char newChar = ALPHABET.charAt(newIndex);
            plainText += newChar;
        }
        plainTxt.setText(plainText);
    }
    private void PlayFairEnc() {
        String PlainText = plainTxt.getText();
        String keyAdjusted = keyAdjust (keyTxt.getText());
        char [][] keyInMatrix=matrix (keyAdjusted);
        String cipher = "";
        String formated = format (PlainText);
        String[] pairs = Divide2Pairs (formated);
        char charOne;
        char charTwo;
        int[] char1Pos;
        int[] char2Pos;
        for (int i=0;i<pairs.length;i++)
        {
            int temp;
            charOne = pairs[i].charAt(0);       
            char1Pos = CharPosition(charOne, keyInMatrix);
            charTwo = pairs[i].charAt(1);
            char2Pos = CharPosition(charTwo, keyInMatrix);
            if (char1Pos[0]==char2Pos[0])
            {
                if (char1Pos[1]<4)
                    char1Pos[1]++;
                else 
                    char1Pos[1]=0;
                if (char2Pos[1]<4)
                    char2Pos[1]++;
                else 
                    char2Pos[1]=0;
            }
            else if (char1Pos[1]==char2Pos[1])
            {
                if (char1Pos[0]<4)
                    char1Pos[0]++;
                else
                    char1Pos[0]=0;
                if (char2Pos[0]<4)
                    char2Pos[0]++;
                else 
                    char2Pos[0]=0;
            }
            else
            {
                 temp = char1Pos[1];
                 char1Pos[1]=char2Pos[1];
                 char2Pos[1]=temp;
            }
         cipher = cipher + 
                 keyInMatrix [char1Pos[0]][char1Pos[1]] + 
                 keyInMatrix [char2Pos[0]][char2Pos[1]];
        }
        cipherTxt.setText(cipher);
    }
    private void PlayFairDec() {
        String cipherText = cipherTxt.getText();
        String keyAdjusted = keyAdjust (keyTxt.getText());
        char [][] keyInMatrix=matrix (keyAdjusted);
        String plain = "";
        String formated = format (cipherText);
        String[] pairs = Divide2Pairs (formated);
        char charOne;
        char charTwo;
        int[] char1Pos;
        int[] char2Pos;
        for (int i=0;i<pairs.length;i++)
        {
            int temp;
            charOne = pairs[i].charAt(0);       
            char1Pos = CharPosition(charOne, keyInMatrix);
            charTwo = pairs[i].charAt(1);
            char2Pos = CharPosition(charTwo, keyInMatrix);
            if (char1Pos[0]==char2Pos[0])
            {
                if (char1Pos[1]>0)
                    char1Pos[1]--;
                else 
                    char1Pos[1]=4;
                if (char2Pos[1]>0)
                    char2Pos[1]--;
                else 
                    char2Pos[1]=4;
            }
            else if (char1Pos[1]==char2Pos[1])
            {
                if (char1Pos[0]>0)
                    char1Pos[0]--;
                else
                    char1Pos[0]=4;
                if (char2Pos[0]>0)
                    char2Pos[0]--;
                else 
                    char2Pos[0]=4;
            }
            else
            {
                 temp = char1Pos[1];
                 char1Pos[1]=char2Pos[1];
                 char2Pos[1]=temp;
            }
         plain = plain + 
                 keyInMatrix [char1Pos[0]][char1Pos[1]] + 
                 keyInMatrix [char2Pos[0]][char2Pos[1]];
        }
        plainTxt.setText(plain);
    }
    private String keyAdjust(String keyWord){
            String alpha = "abcdefghjklmnopqrstuvwxyz";
            String keyTaken ="";
            String key= keyWord.toLowerCase();
            char [] alphabet = alpha.toCharArray();
            ArrayList<Character> Adjusted =new ArrayList<>();
            if (key.charAt(0)=='i')
            Adjusted.add('j');
            else
            Adjusted.add(key.charAt(0));
            
            for(int i = 0;i<key.length();i++){
               if (!Adjusted.contains(key.charAt(i))) 
                   if (key.charAt(i)=='i')
                      Adjusted.add('j');
                   else
                     Adjusted.add(key.charAt(i));
            }
            
            for (Character character : alphabet) {
                if(!Adjusted.contains(character))
                    Adjusted.add(character);
            } 
            for (Character character : Adjusted)
                keyTaken+=character;
            return keyTaken;
    }
    private char[][] matrix (String matrixChars){
        char [][] matrix  = new char[5][5];
        int count = 0;
                String gg = "";
        for (int i=0;i<5;i++)
            for (int j=0;j<5;j++){
                matrix [i][j]=matrixChars.charAt(count);
                count ++;
                gg+= matrix[i][j];
                
            }
        return matrix;
    }
    private String format (String plainText){
      StringBuilder temp = new StringBuilder("");
      for (int i=0;i<plainText.length();i+=1)
          temp.append(plainText.charAt(i));
      for (int i=0;i<plainText.length();i+=2)
          if (temp.charAt(i)==temp.charAt(i+1))
                temp.insert(i+1, 'x');
      plainText = temp.toString();
      
     if (plainText.length()%2!=0)
          plainText  = plainText + 'x';
          
      for (int i=0;i<plainText.length();i++)
          if (plainText.charAt(i) =='i'){
              plainText= plainText.substring(0,i)+'j'+plainText.substring(i+1);
          }
        return plainText;
    }
    private String [] Divide2Pairs (String formatedPlainText){
        int size = formatedPlainText.length()/2;
        String[] x = new String [size];
        int c=0;
        for (int i=0;i<size;i++){
            x[i]=formatedPlainText.substring(c,c+2);
            c+=2;
        }
        return x;
    }
    private int[] CharPosition (char character, char[][] keyInMatrix){
        int[] position = new int [2];
        for (int i=0;i<5;i++)
            for (int j=0;j<5;j++)
                if (keyInMatrix [i][j]==character)
                {
                    position[0]=i;
                    position[1]=j;
                    break;
                }
        return position;
    }
    private void desEnc() {
        String plainText = plainTxt.getText().toLowerCase();
        String key = keyTxt.getText().toLowerCase();
        subKeys (key);
        plainText = permute(plainText,initialPermutation,64);
        prevLeft = plainText.substring(0,plainText.length());
        prevRight = plainText.substring(plainText.length());
        for (int i=0;i<16;i++)
        {
            newLeft = prevRight;
            newRight = function (subKeys.get(i));
            prevLeft = newLeft;
            prevRight = newRight;
        }
    }
    private void subKeys (String key){
        key = permute (key, permutedChoice1, 64);
	prevLeft = key.substring (0,key.length()/2);
	prevRight = key.substring (key.length()/2);
	for (int i=0;i<16;i++)
        {
            newLeft = rotateLeft (prevLeft, shiftingTimes[i]);
            newRight = rotateLeft (prevRight, shiftingTimes[i]);
            prevLeft = newLeft;
            prevRight = newRight;
            newSubkey = newLeft + newRight;
            newSubkey = permute (newSubkey, permutedChoice2, 56);
            subKeys.add(newSubkey);
        }
    }
    private String permute (String received, byte[] table,int size){
        StringBuilder builder = new StringBuilder();
        if (received.length()==size)
        {
            for (byte index : table) {
                builder.append (received.charAt(index-1));
            }
        }
        return builder.toString();
    }
    private String rotateLeft(String prev, int shiftingTimes) {
        return prev.substring(shiftingTimes) + prev.substring(0, shiftingTimes);
    }
    private String function (String key){
        newRight = dBox () ;
        newRight = xOr (newRight,key) ;
        newRight = sBox (newRight) ;
        newRight = permute (newRight, functionPermutation, 32) ;
        newRight = xOr (newRight, prevLeft);
        return newRight;
    }
    private String dBox(){
    newRight= new String ();
        return newRight;
    }
    private String xOr (String one,String two){
        return one;
    }
    private String sBox (String right){
        return right;
    }
}
