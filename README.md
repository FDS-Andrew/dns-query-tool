<h1>dns-query-tool</h1>
<h2>建置:</h2>

<h3>建 Azure app service</h3>

<span style="font-size:12pt">
    <li>stack 使用 python3.9</li>
    <li>deployment center 的地方用</li>
    <u style="color:dodgerblue">https://FreedomSystems@dev.azure.com/FreedomSystems/dns-query-tool/_git/dns-query-tool</u>
    <li>建完後連上 <u style="color:dodgerblue">your_app_name.azurewebsites.net/query</u> 即可使用</li>
    <b style="color:crimson">連結尾端要加/query才能使用</b>
</span>

<h3>ANode.js 12 已不再支援:</h3>
<strike><a style="font-size:16pt" href="https://dnsquery.azurewebsites.net/query/">dnsquery</a></strike>

<h2>備註:</h2>
<span style="font-size:12pt">
    <h3>Django:</h3>
        <li>這個 app 是用 django 寫的，需用到 python、html</li>
        <li>若 python 程式碼要追加外部module，要寫在 <u style="color:dodgerblue">requirements.txt</u></li>
    <h3>Database:</h3>
        <li>有維運的客戶大致上已建database</li>
        <li>Azure app service 有 bug 會干擾 python-sqlite3 的運作，所以輸出的結果可能有誤</li>
        <li>若要更改 <u style="color:dodgerblue">query.db</u> 請用 sqlite3 連進去更改</li>
    <h3>Html:</h3>
        <li>若要改網站版面設計，html 檔在 template 資料夾裡</li>
        <li>html 檔裡出現的 variables 都寫在 <u style="color:dodgerblue">views.py</u> 裡 context 的部分</li>
            <img src="images/context.png" alt="context">
        <li>版面有用到 CSS 要注意</li>
        <li>圖示從 <a href="https://fontawesome.com/">這裡</a> 抓的</li>
        <li>light-mode 的程式碼在 script 裡</li>
            <img src="images/script.png" alt="script">
    <h3>views.py:</h3>
        <li><u style="color:dodgerblue">views.py</u> 在 query 資料夾裡</li>
        <li>index 管理 homepage ( <u style="color:dodgerblue">home.html</u> )</li>
        <h4>search:</h4>
            <li>主要管理answer ( <u style="color:dodgerblue">ans.html</u> )</li>
            <li>取得 domain 名稱跟確認 domain 存在:</li>
                <img src="images/domain.png" alt="get domain name">
            <li>把 sql 的過程簡單化:</li>
                <img src="images/sql.png" alt="sql process">
                <img src="images/database_search.png" alt="database">
            <li>確認 SOA 的 serial 有沒有變:</li>
                <img src="images/soa.png" alt="soa_check">
            <li>若 SOA 有變則建一個新的 table 並把舊的刪掉:</li>
                <img src="images/create_table.png" alt="create_table">
            <li>每個 type 都是一筆將會存取的資料:</li>
                <img src="images/type.png" alt="type">
            <li>A, AAAA, NS, MX, TXT, SOA 的查詢:</li>
                <img src="images/record_search.png" alt="record_search">
            <li>比較 whois 裡的 nameservers 跟 NS record 是否一致:</li>
                <img src="images/whois_ns_compare.png" alt="whois_ns_compare">
            <li>比較 NS record 的 IP 是不是放在同個位置:</li>
                <img src="images/ns_ip_compare.png" alt="ns_ip_compare">
            <li>ASN 的查詢:</li>
                <img src="images/asn.png" alt="asn_search">
            <li>從 <u style="color:dodgerblue">whois.txt</u> parse 出 註冊商 和 到期日:</li>
                <img src="images/regi.png" alt="regi">
                <img src="images/exp.png" alt="exp">
            <br>
            <b style="color:crimson">python-whois 有內建parser但直接將raw data存起來比較方便省時</b>
            <li>用 MX record 來比對 <u style="color:dodgerblue">mail_list.txt</u> 去判定 email provider:</li>
                <img src="images/mail_search.png" alt="mail_search">
            <li>若 email provider 是 microsoft 的話要判定有沒有 office 365 該有的 records:</li>
                <img src="images/o365.png" alt="o365">
            <li>看 domain 有沒有架網站:</li>
                <img src="images/www.png" alt="www_check">
        <h4>whoisdetails:</h4>
            <li>跟 search 裡的 whois_ns_compare 一樣不過錯誤訊息較詳細</li>
        <h4>nsdetails:</h4>
            <li>跟 search 裡的 ns_ip_compare 一樣不過錯誤訊息較詳細</li>
</span>
