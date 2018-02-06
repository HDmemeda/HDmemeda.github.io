## Welcome to the blog of HD
Well Well Well
Nothing to say.
<html> 
    <head>  
        <title>井字棋游戏1.0</title>  
        <script type="text/javascript" src="jinziqi.js"></script>  
    <body>  
  
        <p><b><h2>井字棋对战</h2></b><p>  
        <table border="1" width="50">  
            <tr>  
                <td><input type="button" id="bt7" value="  "width="50" onclick="bn(7)"></td>  
                <td><input type="button" id="bt8" value="  "width="50" onclick="bn(8)"></td>  
                <td><input type="button" id="bt9" value="  "width="50" onclick="bn(9)"></td>  
            </tr>  
            <tr>  
                <td><input type="button" id="bt4" value="  "width="50" onclick="bn(4)"></td>  
                <td><input type="button" id="bt5" value="  "width="50" onclick="bn(5)"></td>  
                <td><input type="button" id="bt6" value="  "width="50" onclick="bn(6)"></td>  
            </tr>  
            <tr>  
                <td><input type="button" id="bt1" value="  "width="50" onclick="bn(1)"></td>  
                <td><input type="button" id="bt2" value="  "width="50" onclick="bn(2)"></td>  
                <td><input type="button" id="bt3" value="  "width="50" onclick="bn(3)"></td>  
            </tr>  
        </table>  
        <br>  
        <input type="text" id="info" value="游戏开始!玩家先行!" disabled="true">  
        <br><br>  
        <input type="button" id="restart" value="重新开始" onclick="restart()">  
        <input type="button" id="enableAI" value="关闭AI" onclick="cgAI()">  
        <br>  
        <br>O胜利：<input type="text" id="o_win" value="0" disabled="true">  
        <br>X胜利：<input type="text" id="x_win" value="0" disabled="true">  
        <br>_平局：<input type="text" id="draw" value="0" disabled="true">  
        <br>  
  
    </body>  
</html>  
<script>
var jin = new Array(0,0,0,0,0,0,0,0,0,0);//井字格，O为1，X为-1  
var XorO = 0;//轮到O还是X下棋  
var enableAI = 1;//默认启用AI  
var gameover = false;//游戏是否结束  
var player_won = 0;  
var AI_won = 0;  
var draw =0;  
  
function AI(){  
 var i=0;
 do{i=Math.floor(Math.random()*10)}while(jin[i]!=0);
    bn(i);  
}  
function bn(i){  
    if(jin[i]!=0 || gameover)return ;//游戏结束时或该棋格已被下过  
    if(XorO==0){  
        if(i==1)document.getElementById("bt1").value="O";  
        else if(i==2)document.getElementById("bt2").value="O";  
        else if(i==3)document.getElementById("bt3").value="O";  
        else if(i==4)document.getElementById("bt4").value="O";  
        else if(i==5)document.getElementById("bt5").value="O";  
        else if(i==6)document.getElementById("bt6").value="O";  
        else if(i==7)document.getElementById("bt7").value="O";  
        else if(i==8)document.getElementById("bt8").value="O";  
        else if(i==9)document.getElementById("bt9").value="O";  
        jin[i]=1;  
    }  
    else{  
        if(i==1)document.getElementById("bt1").value="X";  
        else if(i==2)document.getElementById("bt2").value="X";  
        else if(i==3)document.getElementById("bt3").value="X";  
        else if(i==4)document.getElementById("bt4").value="X";  
        else if(i==5)document.getElementById("bt5").value="X";  
        else if(i==6)document.getElementById("bt6").value="X";  
        else if(i==7)document.getElementById("bt7").value="X";  
        else if(i==8)document.getElementById("bt8").value="X";  
        else if(i==9)document.getElementById("bt9").value="X";  
        jin[i]=-1;  
    }  
    cgTurn();  
}  
function cgTurn(){  
    var sum=0;  
    for(var i=0;i<10;i++)if(jin[i]!=0)sum++;  
      
    if( checkWin()==true ){  
        gameover=true;  
        if(XorO==0){  
            document.getElementById("info").value="O胜利!";  
            player_won++;balance();  
        }  
        else {  
            document.getElementById("info").value="X胜利!";  
            AI_won++;balance();  
        }  
        return ;  
    }  
    if(sum==10){  
	gameover=true;
        document.getElementById("info").value="平局!";  
        draw++;balance();  
        return ;  
    }  
    XorO=(XorO+1)%2;  
    if(XorO==0)document.getElementById("info").value="轮到O";  
    else {  
        document.getElementById("info").value="轮到X";  
        if(enableAI==1)AI(); 
    }  
	return;
}  
function checkWin(){  
    var num=false;  
    if(jin[7]+jin[8]+jin[9]==-3 || jin[7]+jin[8]+jin[9]==3)return true;  
    else if(jin[4]+jin[5]+jin[6]==-3 || jin[4]+jin[5]+jin[6]==3)return true;  
    else if(jin[1]+jin[2]+jin[3]==-3 || jin[1]+jin[2]+jin[3]==3)return true;  
    else if(jin[1]+jin[4]+jin[7]==-3 || jin[1]+jin[4]+jin[7]==3)return true;  
    else if(jin[2]+jin[5]+jin[8]==-3 || jin[2]+jin[5]+jin[8]==3)return true;  
    else if(jin[3]+jin[6]+jin[9]==-3 || jin[3]+jin[6]+jin[9]==3)return true;  
    else if(jin[1]+jin[5]+jin[9]==-3 || jin[1]+jin[5]+jin[9]==3)return true;  
    else if(jin[7]+jin[5]+jin[3]==-3 || jin[7]+jin[5]+jin[3]==3)return true;  
}  
function restart(){  
    for(i=1;i<10;i++)jin[i]=0;  
    document.getElementById("bt1").value="  ";  
    document.getElementById("bt2").value="  ";  
    document.getElementById("bt3").value="  ";  
    document.getElementById("bt4").value="  ";  
    document.getElementById("bt5").value="  ";  
    document.getElementById("bt6").value="  ";  
    document.getElementById("bt7").value="  ";  
    document.getElementById("bt8").value="  ";  
    document.getElementById("bt9").value="  ";  
    document.getElementById("info").value="游戏开始!玩家先行!"  
    XorO = 0;  
    gameover=false;  
}   
function cgAI(){  
    enableAI=(enableAI+1)%2;  
    if(enableAI==0)document.getElementById("enableAI").value="开启AI";  
    else document.getElementById("enableAI").value="关闭AI";  
}  
//结算、更新界面  
function balance(){  
    document.getElementById("o_win").value=player_won;  
    document.getElementById("x_win").value=AI_won;  
    document.getElementById("draw").value=draw;  
}  
</script>









