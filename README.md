define(‘LINE_API’,”https://notify-api.line.me/api/notify");
 
$token = “”; //ใส่Token ที่copy เอาไว้
$str = “สำหรับการประเมินความสุขบุคลากร (Happinometer) ระบบเปิดระหว่าง 1 พ.ย. 61 - 31 ม.ค. 62 

กลุ่มเป้าหมายที่ต้องตอบแบบประเมิน ประกอบด้วย
1. ข้าราชการ
2. พนักงานราชการ
3. ลูกจ้างประจำ
4. พนักงานกระทรวง
5. ลูกจ้างชั่วคราว (ไม่รวมลูกจ้างโครงการและพนักงานจ้างเหมา)

สามารถเข้าตอบแบบประเมินได้ที่ happinometer.moph.go.th

ทั้งนี้ หากมีข้อสงสัยเพิ่มเติม สามารถติดต่อได้ที่ งานพัฒนานโยบายด้านบริหารและระบบบริการ กลุ่มพัฒนานโยบายด้านสุขภาพ กองยุทธศาสตร์และแผนงาน สำนักงานปลัดกระทรวงสาธารณสุข โทร. 0-2590-2459 (ในเวลาราชการ) หรือ E-mail: spd.policy@gmail.com  Inbox Facebook: HR4Health หรือ SPDMOPHThai”; //
 
$res = notify_message($str,$token);
print_r($res);
function notify_message($message,$token){
 $queryData = array(‘message’ => $message);
 $queryData = http_build_query($queryData,’’,’&’);
 $headerOptions = array( 
         ‘http’=>array(
            ‘method’=>’POST’,
            ‘header’=> “Content-Type: application/x-www-form-urlencoded\r\n”
                      .”Authorization: Bearer “.$token.”\r\n”
                      .”Content-Length: “.strlen($queryData).”\r\n”,
            ‘content’ => $queryData
         ),
 );
 $context = stream_context_create($headerOptions);
 $result = file_get_contents(LINE_API,FALSE,$context);
 $res = json_decode($result);
 return $res;
}
