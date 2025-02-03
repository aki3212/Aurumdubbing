<?php


ob_start();
error_reporting(0);
define('API_KEY','7732735098:AAGxwi1lMhqlw4GfWNo6mcQ8TgHpGvQ5ltU');  
$admin = 5461037221;
$kanali = "https://t.me/aurumdubbing";
$bot = "aurumuzbot"; //@belgisini qoʻymasdan
$admen = "Aki3212"; //@ Belgisini qoʻymasdan

$reklama = "anime  @aurumdubbing orqali yuklandi"; 

function bot($method,$datas=[]){
$url = "https://api.telegram.org/bot".API_KEY."/".$method;
$ch = curl_init();
 curl_setopt($ch,CURLOPT_URL,$url);
 curl_setopt($ch,CURLOPT_RETURNTRANSFER,true);
 curl_setopt($ch,CURLOPT_POSTFIELDS,$datas);
 $res = curl_exec($ch);
 if(curl_error($ch)){
  var_dump(curl_error($ch));
 }else{
  return json_decode($res);
}
}

$botss = file_get_contents("https://api.telegram.org/bot".$token."/getme");
$jsons = json_decode($botss);
$botusername = $jsons->result->username;


$update = json_decode(file_get_contents("php://input"));
$message = $update->message;
$doc = $message->document;
$file_id = $doc->file_id;
$file_name = $doc->file_name;
$size = $doc->file_size;
$dtype= $doc->mime_type;

$chat_id = $message->chat->id;
$mid = $message->message_id;
$text = $message->text;  
$firstname = $message->chat->first_name;
$lastname = $message->chat->last_name;
$query = $update->inline_query->query; 
$infid = $update->inline_query->from->id;
$inid = $update->inline_query->id;
$incid = $update->inline_query->chat->id;
$inmid = $update->inline_query->message->id;
$cqid = $update->callback_query->id;
$uid= $message->from->id;
$ccid = $update->callback_query->message->chat->id;
$data = $update->callback_query->data;
$query=$update->inline_query->query;
$step=file_get_contents("step/$chat_id.txt");
$kanal=file_get_contents("stat/kanal.txt");
$mid = $message->message_id;
mkdir(step);



$type = $message->chat->type;
$chat_id = $message->chat->id;
$idi = $message->from->id;
$id = $update->callback_query->id;
$callcid = $update->callback_query->message->chat->id;
$mes_idi = $update->callback_query->message->message_id;  
$from_id = $update->callback_query->from->id;
$callmid = $update->callback_query->message->message_id;  
$callcid = $update->callback_query->message->chat->id;



$kanal1=file_get_contents("@aurumdubbing"); // kanaliz useri
$kanal2=file_get_contents("ch2.txt"); // kanaliz useri
$kanal3=file_get_contents("ch3.txt"); // kanaliz useri
$kanal4 = file_get_contents("ch4.txt");
$admins = file_get_contents("admins.txt");

$first_name = $message->from->first_name;
$username = $message->from->username;
if(isset($message)){
    $users = file_get_contents("azolar.txt");
    $azolar_soni = substr_count($users,"\n");
    if(!preg_match("/$chat_id/i", "$users")){
        file_put_contents("azolar.txt", "$users\n$chat_id");
        bot('sendMessage', [
            'chat_id' => 5819317484,
            'text' => "🤖Botga yangi a'zo qo'shildi
✅ User: @$username
🆔 ID: <code>$chat_id</code>
✉️ Lichka: <a href='tg://user?id=$chat_id'>$first_name</a>

👥 Jami azolar: $azolar_soni ta bo'ldi",
            'parse_mode' => "html",
        ]);
    }
}

$joinchatid = $update->chat_join_request->chat->id;
$chatjoinname = $update->chat_join_request->chat->title;
$chatjoinuser = $update->chat_join_request->chat->username;
$chatjoinlink = $update->chat_join_request->chat->invite_link;
$qb= $update->chat_join_request->from->id;
$fjname= $update->chat_join_request->from->first_name;
$ty = $update->chat_join_request->chat->type;
if(isset($joinchatid)){
    
// bot("approveChatJoinRequest",[
// "chat_id"=>$joinchatid,
// "user_id"=>$qb,
// ]);
$getza = file_get_contents("stat/$joinchatid.txt");
if(!preg_match("/$qb/i", $getza)){
    file_put_contents("stat/$joinchatid.txt", "$getza\n$qb");
}

}
function getName($id){
    $getname = bot('getchat',['chat_id'=>$id])->result->first_name;
    if(!empty($getname)){
        return $getname;
    }else{
        return bot('getchat',['chat_id'=>$id])->result->title;
    }
}
function joinchat($id){
global $mid;
$array = array("inline_keyboard");
$get = file_get_contents("stat/kanal.txt");
$ex = explode("\n",$get);

		if($get=="0" or $get==""){  
			return true;
		$uns = false;
		}else{
if(true){
for($i=0;$i<=count($ex)-2;$i++){
	$s=$i+1;
	$first_line = $ex[$s];
	
if(preg_match("/\@/i", $first_line)){
    $first_ex = explode("@",$first_line);
    $urlt = "@".$first_ex[1];
    $url = "https://t.me/".$first_ex[1];
    
    $name = getName($urlt);
     $ret = bot("getChatMember",[
         "chat_id"=>$urlt,
         "user_id"=>$id,
         ]);
$stat = $ret->result->status;
}else{
    $first_ex = explode("++",$first_line);
    $urlt = $first_ex[0];
    $name = getName($urlt);
    $url = $first_ex[1];
    $getz = file_get_contents("stat/$urlt.txt");
    if(preg_match("/$id/i", $getz)){
        $stat = "member";
    }else{
        $stat = "left";
    }
}


         if((($stat=="creator" or $stat=="administrator" or $stat=="member"))){
      $array['inline_keyboard']["$i"][0]['text'] = "✅ ".$name;
$array['inline_keyboard']["$i"][0]['url'] = "$url";

         }else{
$array['inline_keyboard']["$i"][0]['text'] = "❌ ".$name;
$array['inline_keyboard']["$i"][0]['url'] = "$url";

$uns = true;
}


}
$get = file_get_contents("stat/kanal.txt");
$all=substr_count($get,"\n");
$array['inline_keyboard'][$all][0]['text'] = "🔄 TEKSHIRISH";
$array['inline_keyboard'][$all][0]['callback_data'] = "obuna";
}

$get = file_get_contents("admin/kanal/kanal.txt");
if($uns == true){
     bot('sendMessage',[
         'chat_id'=>$id,
         'reply_to_message_id' => $mid,
         'text'=>"<b>🤖 Botdan to'liq foydalanish uchun</b> quyidagi kanallarga obuna bo'ling👇 va qayta /start bosing",
'parse_mode'=>"html",
'disable_web_page_preview'=>true,
'reply_markup'=>json_encode($array),
]);  
return false;
}else{
return true;
}

if($uns == false){
return true;
}

}
}


if($text=="/start" and joinchat($chat_id)){
bot('sendmessage',[
'chat_id'=>$chat_id,
'text'=>"👋 Salom $firstname !

Marhamat, kerakli kodni yuboring:",
"reply_markup"=>json_encode([
'inline_keyboard'=>[
[['text'=>"🔎Kodlarni qidirish", 'url'=>"$kanali"]],
]])
]);
}
$data = $update->callback_query->data;
$cmid = $update->callback_query->message->message_id;
$ccid = $update->callback_query->message->chat->id;
$ctext = $update->callback_query->message->text;
$cfid = $update->callback_query->message->from->id;
$qid = $update->callback_query->id; 

$ctext = $update->callback_query->message->text; 
$callfrid = $update->callback_query->from->id; 
$callfname = $update->callback_query->from->first_name;  
$calltitle = $update->callback_query->message->chat->title; 
$calluser = $update->callback_query->message->chat->username; 
$callfuser = $update->callback_query->from->username; 
if($data == "obuna"){
    if(joinchat($callfrid) == true){
    bot('editMessageText',[
	'chat_id'=>$ccid,
	"message_id" => $cmid,
	'parse_mode'=>'html',
'text'=>"👋 Salom Siz muvafaqqiyatli tasdiqlandingiz!

Marhamat, kerakli kodni yuboring:",
"reply_markup"=>json_encode([
'inline_keyboard'=>[
[['text'=>"🔎Kodlarni qidirish", 'url'=>"$kanali"]],
]])
	]);
    }else{
            bot('answerCallbackQuery',[ 
        'callback_query_id'=>$qid, 
        'text'=>"❗Kanalimizga  obuna bo'lib qayta urinib ko'ring", 
        'show_alert'=>true,
    ]);
        bot('deletemessage',[ 
            'chat_id'=>$ccid, 
            "message_id" => $cmid,
        ]);
    }
}

if($text=="🎥Kino qoʻshish" or $step=="kadd" or $text=="/panel" or $text=="📄 Kanallar Ro'yhati" or $text=="📊 Statistika" or $text=="➕ Kanal Qo'shish" or $text=="🗑 Kanallarni O'chirish" or  text!="📣 Reklama jonatish" or $text=="📢 Kanallar boshqaruvi"  or $text=="/start" or isset($message->video)){

}

if(is_numeric($text) and joinchat($chat_id)){
$apksoni = file_get_contents("stat/soni.txt");
if(preg_match("/$text/i", $apksoni)){
    $start = explode("/start ","$text");
$startlink = $start[1];
    
    $apkbaza = file_get_contents("stat/apk.txt");
$apkbazalink = explode("$text#","$apkbaza");
$apkfile = $apkbazalink[1];

$apkbazalink = explode("##","$apkfile");
$apkfile = $apkbazalink[0];
$file_name = $apkbazalink[4];
$size = $apkbazalink[1];
// 	bot('sendmessage',[
// 'chat_id'=>$admin,
// 'text'=>"$apkfile",
// ]);

	bot('sendvideo',[
'chat_id'=>$chat_id,
'video'=>"$apkfile",
'caption'=>"🎥Kino kodi: $text

$reklama",
'parse_mode'=>"html",
]);
}else{
    
bot('sendmessage',[
'chat_id'=>$chat_id,
'text'=>"Bunday kodli kino topilmadi",
]);
}
}



if(isset($message->video) and $chat_id==$admin){
$caption = $message->caption;
$doc = $message->video;
$file_id = $doc->file_id;
$file_name= $doc->file_name;
$file_size = $doc->file_size;
$size=$file_size/1000000;
$dtype = $doc->mime_type;
$apkstat = file_get_contents("stat/apk.txt");
if(mb_stripos("$apkstat", "$file_id")){
    bot('sendmessage',[
'chat_id'=>$chat_id,
'text'=>"Bu kino oldin bazaga saqlangan",
]);
}else{
    

$rand = rand(0000,9999);
$apksoni = file_get_contents("stat/soni.txt");
if(preg_match("/$rand/i", $apksoni)){
    $rand2 = rand(0000,9999);
    $apksonie = $rand2;
    
file_put_contents("stat/soni.txt", "$apksoni\n$rand2");
}else{
    $apksonie = $rand;
file_put_contents("stat/soni.txt", "$apksoni\n$rand");
}

bot('sendmessage',[
'chat_id'=>$chat_id,
'text'=>"🎥Kino kodi: <code>$apksonie</code>

📲Video Hajmi: $size Mb",
'parse_mode'=>"html",
]);

$apkstat = file_get_contents("stat/apk.txt");
file_put_contents("stat/apk.txt","$apkstat\n$apksonie#$file_id##");
}
}









################### ADMIN PANEL ######################
################Panel ##################

if($text=="/panel" and $chat_id==$admin){
unlink("step/$chat_id.txt");
bot('sendMessage',[
'chat_id'=>$chat_id,
'text'=>"Panelga hush kelibsiz Hurmatli $firstname 👮",
'parse_mode'=>'html',
'reply_markup'=>json_encode([
'resize_keyboard'=>true,
'keyboard'=>[
[['text'=>"🎥Kino qoʻshish"]],
[['text'=>"📊 Statistika"],['text'=>"📢 Kanallar boshqaruvi"]],
[['text'=>"📣 Reklama jonatish"],['text'=>"/start"]],
],
]),
]);
}elseif($text=="/panel" and $chat_id!=$admin){
    bot('sendMessage',[
'chat_id'=>$chat_id,
'text'=>"Kechirasiz bu boʻlimga faqat bot admini kiroladi",
'parse_mode'=>'html',
'reply_markup'=>json_encode([
'resize_keyboard'=>true,
'keyboard'=>[
[['text'=>"/start"]],
],
]),
]);
}


// ############# Statistika #############

if($text== "📊 Statistika" and $chat_id == $admin || $chat_id == $admins){
      $baza=file_get_contents("azolar.txt");
      $all=substr_count($baza,"\n");
      $txx = "🤖Botdagi jami azolar soni: $all ta";
  bot('sendmessage',[
   'chat_id'=>$chat_id,
   'parse_mode'=>'html',
   'text'=>$txx,
  ]);
}
// ########### Kanallar boshqaruvi ############

mkdir("stat");
if($text=="📢 Kanallar boshqaruvi" and $chat_id==$admin || $chat_id==$admins){
bot("sendMessage",[
"chat_id"=>$chat_id,
"text"=>"📢 Ushbu boʻlimda siz majburiy kanallar ulasangiz boʻladi 

Kanallarni targʻib qiling:",
"parse_mode"=>"html",
'reply_markup'=>json_encode([
'resize_keyboard'=>true,
'keyboard'=>[
[['text'=>"➕ Kanal Qo'shish"],['text'=>"🗑 Kanallarni O'chirish"]],
[['text'=>"📄 Kanallar Ro'yhati"],['text'=>"/panel"]],
]])
]);
}

if($text== "➕ Kanal Qo'shish" and $chat_id == $admin){
file_put_contents("step/$chat_id.txt", "kadd");
  bot('sendmessage',[
   'chat_id'=>$chat_id,
   'parse_mode'=>'html',
   'text'=>"Majburiy kanal qoʻshish uchun kanal @username sini yuboring
   
Majburiy zayafka kanal qo'shish uchun <code>-100kanalidsi++https://t.me/zayafka_linki</code>",
  ]);
}

if($step=="kadd" and $chat_id == $admin and $text!= "➕ Kanal Qo'shish" and $text != "🗑 Kanallarni O'chirish" and $text!= "📄 Kanallar Ro'yhati" and $text!= "/panel"){
unlink("step/$chat_id.txt");
file_put_contents("stat/kanal.txt", "$kanal\n$text");
  bot('sendmessage',[
   'chat_id'=>$chat_id,
   'parse_mode'=>'html',
   'text'=>"$text kanali muvaffaqiyatli qoʻshildi",
  ]);
}

if($text== "🗑 Kanallarni O'chirish" and $chat_id == $admin){
unlink("stat/kanal.txt");
//file_put_contents("stat/kanal.txt", "0");
  bot('sendmessage',[
   'chat_id'=>$chat_id,
   'parse_mode'=>'html',
   'text'=>"Majburiy kanallar muvaffaqiyatli oʻchirildi",
  ]);
unlink("step/$chat_id.txt");
} 

if($text== "📄 Kanallar Ro'yhati" and $chat_id == $admin){
   $all2=substr_count($kanal,"\n");
  bot('sendmessage',[
   'chat_id'=>$chat_id,
   'parse_mode'=>'html',
   'text'=>"Majburiy kanallar roʻyxati
$kanal

kanallar $all2 ta",
  ]);
unlink("step/$chat_id.txt");
}

if($text== "🎥Kino qoʻshish" and $chat_id == $admin){
  bot('sendmessage',[
   'chat_id'=>$chat_id,
   'parse_mode'=>'html',
   'text'=>"Marhamat kinoni shu botga yuboring keyin bot kinoga yuklab olish kodini beradi",
  ]);
}
############# Reklama yuborish ##################


if($text=="📣 Reklama jonatish" and $chat_id==$admin){
bot('sendmessage',[
'chat_id'=>$chat_id,
'text'=>"
👥Userlarga Yuboriladigan 
📄Xabar Matnini Kiriting! 
🚫Bekor qilish uchun /cancel ni bosing.",
'parse_mode'=>"html",
]); 
file_put_contents("send.txt","user");
}
$xabar = file_get_contents("send.txt");
if($xabar=="user" and $chat_id==$admin and $text!="📣 Reklama jonatish"){
if($text=="/cancel"){
   bot('sendmessage',[
    'chat_id'=>$chat_id,
    'text'=>"Bekor qilindi!",
    'parse_mode'=>"html",
]);
unlink("send.txt");
}else{
  $lich = file_get_contents("azolar.txt");
  $lichka = explode("\n",$lich);
  foreach($lichka as $lichkalar){
  $okuser=bot("sendmessage",[
    'chat_id'=>$lichkalar,
    'text'=>$text,
    'parse_mode'=>'html',
]);
}
if($okuser){
  bot("sendmessage",[
    'chat_id'=>$chat_id,
    'text'=>"Xabar yuborish tugadi",
    'parse_mode'=>'html',
]);
unlink("send.txt");
}
}
}

?>
