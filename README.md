# -ZCSP.Page
Супер-класс позволяющий работать с CSP страницами в рамках оного процесса(идентификация по  IP адресу) 
    Глобальные переменные:
       %ClientIP 
       %ProcessID
    
    <br> <!--  <script language="JavaScript" type="text/javascript" src="%25ZCSP.Page.cls?ProcessID=ИдентификаторПроцессаККоторомуБудемПодключатся"></script>  -->
    <br> <!--  <script language="JavaScript" type="text/javascript" src="%25ZCSP.Page.cls/?include=#(##this)#"></script> -->
    <br> <!--  <script language="JavaScript" type="text/javascript" src="%25ZCSP.Page.cls/?ProcessID=ИдентификаторПроцесса&interval=1000"></script> -->
    <pre> 
    Пример для ПК SIRENA
      &lt;script language="JavaScript" type="text/javascript" src="#($SYSTEM.CSP.GetDefaultApp($ZU(5)))#/#($zcvt("%ZCSP.Page","O","URL"))#.cls?ProcessID=#($zu(5))#&interval=15000"&gt;&lt;/script&gt;
      <!--  <script language="JavaScript" type="text/javascript" src="#($SYSTEM.CSP.GetDefaultApp($ZU(5)))#/#($zcvt("%ZCSP.Page","O","URL"))#.cls?ProcessID=#($zu(5))#&interval=15000"></script>  -->
    
    Закрыть процесс на сервере
      #server(logout())#
    
    Прочитать сообщение с сервера
      #server(read())#
    
    Оставить JS сообщение пользователю
      d ##class(%ZCSP.Page).SendJS("10.20.29.67","alert(11)","SIRENA")
      d ##class(%ZCSP.Page).SendJS("10.20.29.67","alert(11)")
    
    Разлогинить себя из кода 
     d ##class(%ZCSP.Page).logout()
    
    Принудительно отключить всех пользователей
      d ##class(%ZCSP.Page).CloseAllProcess()
    
    <example>  
     Class User.main Extends %ZCSP.Page
     {
     
     ClassMethod main()
     {
        w $h_"  "_$job
      &html<
           <script language='JavaScript'>
           alert('#($h_"    "_$job)#');
           if(typeof Android != "undefined"){  Android.alert('#($h_"    "_$job)#');}  
           alert(test());
          </script>
       >
       w $c(13,10),"  <script language='JavaScript'>"
       &js<
           alert('#($h_"    "_$job)#');
       >
       w $c(13,10),"</script>"
      
       w "<pre>"
       zw 
       w !,!
       zw %request
       w "</pre>"
      }
     ClassMethod test() As %String [ Language = cache, WebMethod ]
     {
       w $h
       q ""
     }
    }
    </example> 
    </pre>
