<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            margin-left: auto;
            margin-right: auto;
            padding: 0;
            height: 100vh;
            overflow: hidden;
            justify-content: center;
            align-items: center;
            background-color: #F0F4F8; /* Xám xanh nhạt */
            font-size: 16px;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; /* Font chữ hiện đại hơn */
        }

        .container {
            position: relative;
            width: 1600px;
            height: 900px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1); /* Đổ bóng mạnh hơn và mềm mại hơn */
            background-color: #FFFFFF; /* Nền trắng */
            overflow: hidden;
            border-radius: 40px;
            /* top, left, transform giữ nguyên để căn giữa */
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        .traffic-light {
            position: absolute;
            width: 100px;
            height: 300px;
            border: 2px solid #000; /* Có thể bỏ border nếu muốn tối giản */
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            background-color: #343A40; /* Xám đen */
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3); /* Thêm đổ bóng cho cột đèn */
        }

        .traffic-light1 {
            left: 10px;
            top: 40%;
        }

        .traffic-light2 {
            left: 230px;
            top: 65%;
            transform: rotate(270deg);
        }

        .red-light, .yellow-light, .green-light {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            margin: 10px;
            cursor: pointer;
            transition: all 0.2s ease-in-out; /* Chuyển động mượt mà hơn */
            /* Màu mặc định khi tắt */
            background-color: rgba(169, 169, 169, 0.3); /* Đèn mờ khi tắt */
        }


        .red-light[style*="red"], .yellow-light[style*="yellow"], .green-light[style*="green"] {
    box-shadow: 0 0 20px 5px currentColor; /* Hiệu ứng phát sáng */
}


        .red-light { background-color: red; }
        .yellow-light { background-color: yellow; }
        .green-light { background-color: green; }

                .thoigian {
            position: absolute;
            font-weight: bold;
            font-size: 72px;
            color: #2C3E50; /* Xanh đen đậm */
            border-radius: 10px;
            padding: 5px 15px;
        }

        .thoigian1 {
            top: 30%;
            left: 25px;
        }

        .thoigian2 {
            top: 75%;
            left: 440px;
            transform: rotate(90deg);
        }
        

        .caidat-label {
            font-size: 45px; /* Điều chỉnh kích thước hợp lý */
            font-weight: bold;
            color: #34495E; /* Xám xanh đậm */
            margin-bottom: 15px;
            text-align: center;
            width: 100%; /* Đảm bảo căn giữa text */
        }

        .nhapgt {
            position: absolute;
            left: 920px;
            top: 380px;
            display: flex;
            flex-direction: column;
            align-items: flex-start;
        }

        .input-group {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }

        .time {
            font-weight: bold;
            font-size: 45px;
            margin-right: 10px;
        }

        .onhap4 {
            padding: 10px 15px;
            border: 1px solid #BDC3C7; /* Viền xám nhạt */
            border-radius: 8px; /* Bo tròn hơn */
            font-size: 24px !important; /* Đảm bảo kích thước chữ lớn */
            width: 250px; /* Chiều rộng cố định */
            box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1); /* Đổ bóng trong để tạo chiều sâu */
        }

        .annut4 {
            margin-top: 0; /* Bỏ margin-top thừa */
            margin-left: 15px; /* Khoảng cách với input */
            padding: 12px 25px; /* To hơn một chút */
            display: block;
            position: relative;
            bottom: 0; /* Bỏ chỉnh bottom */
            left: 0; /* Bỏ chỉnh left */
            border-radius: 8px; /* Bo tròn đồng bộ */
            box-shadow: 0 3px 7px rgba(0, 0, 0, 0.2); /* Đổ bóng mạnh hơn */
            cursor: pointer;
            border: none;
            background-color: #28A745; /* Xanh lá cây */
            color: white;
            font-size: 20px;
            font-weight: bold;
            transition: background-color 0.2s ease, transform 0.1s ease; /* Hiệu ứng hover */
        }


        .annut4:hover {
            background-color: #218838; /* Xanh lá đậm hơn khi hover */
            transform: translateY(-1px); /* Nâng nhẹ lên khi hover */
        }

        .toggle-switch {
            position: relative;
            top: 10px; /* Điều chỉnh vị trí */
            display: inline-block;
            width: 120px; /* Rộng hơn một chút */
            height: 60px; /* Cao hơn một chút */
            margin-top: 20px; /* Khoảng cách với phần trên */
        }

        .toggle-switch input { display: none; }

        .toggle-switch label {
            display: block;
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #CED4DA; /* Xám nhạt khi tắt */
            border-radius: 30px; /* Bo tròn hơn */
            transition: background-color 0.3s;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.2); /* Đổ bóng trong */
        }

        .toggle-switch label:before {
            content: '';
            position: absolute;
            height: 90%; /* Kích thước nút tròn */
            width: 45%; /* Kích thước nút tròn */
            left: 5%; /* Căn chỉnh vị trí */
            top: 5%; /* Căn chỉnh vị trí */
            background-color: white;
            border-radius: 50%; /* Làm tròn hoàn hảo */
            transition: transform 0.3s;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2); /* Đổ bóng cho nút tròn */
        }

        .toggle-switch input:checked + label {
            background-color: #4CAF50; /* Xanh lá đậm khi bật */
        }

        .toggle-switch input:checked + label:before {
            transform: translateX(100%); /* Di chuyển nút tròn sang phải */
            left: 5%; /* Giữ nguyên vị trí ban đầu của left, chỉ thay đổi transform */
        }

        .trangthai {
            position: relative;
            left: 150%;
            font-size: 36px; /* Điều chỉnh kích thước chữ */
            font-weight: bold;
            white-space: nowrap;
            color: #34495E; /* Xám xanh đậm */
        }

        .chuki {
            position: relative;
            left: 57.5%;
            top: 19%;
            font-size: x-large;
            color: #4A69BD;
            font-family: 'Times New Roman', Times, serif;
        }

        .ten {
            text-align: center;
            font-size: 60px;
        }

        /* New CSS */
        .time1 {
            font-size: 45px;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .caidat-label {
            font-size: 50px;
            font-weight: bold;
            margin-bottom: 10px;
            text-align: center;
        }
        .TT {
            left: 150%;
            margin-top: 5%;
            white-space: nowrap;
            font-size: 20px;
            font-weight: bold;
            color: #34495E; /* Xám xanh đậm */
        }
    </style>
    <title>HỆ THỐNG KIỂM SOÁT ĐÈN GIAO THÔNG</title>
</head>
<script>
    function updatedata() {
        var xhttp = new XMLHttpRequest();
        xhttp.onreadystatechange = function() {
            if (this.readyState == 4 && this.status == 200) {
                var DataVDK = xhttp.responseText;
                console.log("DỮ LIỆU VDK:" + DataVDK);
                var DataJson = JSON.parse(DataVDK);
                updateLEDs(DataJson);
                if(DataJson.GT1 != null)
                {
                    document.getElementById("VL1").innerHTML = DataJson.GT1;
                }
                if(DataJson.GT2 != null)
                {
                    document.getElementById("VL2").innerHTML = DataJson.GT2;
                }
                if(DataJson.GT3 != null)
                {
                    document.getElementById("VL3").innerHTML = DataJson.GT3;
                }
                if(DataJson.GT4 != null)
                {
                    document.getElementById("VL4").innerHTML = DataJson.GT4;
                }
                if(DataJson.GT5 != null)
                {
                    document.getElementById("VL5").innerHTML = DataJson.GT5;
                }
                if(DataJson.TONG != null)
                {
                    document.getElementById("TONG").innerHTML = DataJson.TONG;
                }
                if(DataJson.MODE != null) {
                    document.getElementById("myToggle").checked = (DataJson.MODE == 1);
                    document.getElementById("toggleText").innerText = (DataJson.MODE == 0) ? "CHẾ ĐỘ THỦ CÔNG" : "CHẾ ĐỘ TỰ ĐỘNG";
                }
                if(DataJson.TTN != null) {
                    let statusText = "";
                    switch(parseInt(DataJson.TTN)) {
                        case 0:
                            statusText = "KHÔNG CÓ NGƯỜI";
                            break;
                        case 1:
                            statusText = "ÍT NGƯỜI";
                            break;
                        case 2:
                            statusText = "VỪA NGƯỜI";
                            break;
                        case 3:
                            statusText = "ĐÔNG NGƯỜI";
                            break;
                        default:
                            statusText = "KHÔNG XÁC ĐỊNH";
                    }
                    document.getElementById("TT").innerHTML = statusText;
                }
            }
        }
        xhttp.open('GET', '/Update', true);
        xhttp.send();
        setTimeout(function() { updatedata() }, 1000);
    }

    function updateLEDs(DataJson) {
        const gtLedMapping = {
            'GT6': 'led1',
            'GT7': 'led2',
            'GT8': 'led3',
            'GT9': 'led4',
            'GT10': 'led5',
            'GT11': 'led6',
        };

        for (const gt in gtLedMapping) {
            const ledId = gtLedMapping[gt];
            const value = DataJson[gt];
            updateLED(ledId, value);
        }
    }

    function updateLED(ledId, value) {
        var ledElement = document.getElementById(ledId);
        if (value != null) {
        if (value == 1) {
            ledElement.style.backgroundColor = getLEDColor(ledId);
            ledElement.style.boxShadow = `0 0 20px 5px ${getLEDColor(ledId)}`;
        } else {
            ledElement.style.backgroundColor = 'rgba(169, 169, 169, 0.3)';
            ledElement.style.boxShadow = 'none';
        }
    }
    }

    function getLEDColor(ledId) {
        switch (ledId) {
            case 'led1': return 'red';
            case 'led2': return 'yellow';
            case 'led3': return 'green';
            case 'led4': return 'red';
            case 'led5': return 'yellow';
            case 'led6': return 'green';
            default: return 'rgba(169, 169, 169, 0.5)';
        }
    }

    function sendCommand(key, value) {
        var xhttp = new XMLHttpRequest();
        var queryParam = key + "=" + encodeURIComponent(value); // encodeURIComponent để xử lý ký tự đặc biệt
        xhttp.open('GET', "/input?" + queryParam, true);
        xhttp.send();
        console.log("Sent: /input?" + queryParam);
    }

    function caidatChuKy() {
        var value = document.getElementById("caidat4").value;
        if (value === "" || isNaN(value)) {
            alert("Vui lòng nhập một giá trị số hợp lệ cho chu kỳ.");
            return;
        }
        sendCommand("tong", value); // Gửi với key 'tong'
    }

    function toggleSwitch() {
        var toggle = document.getElementById("myToggle");
        var value = toggle.checked ? 1 : 0; // 1 cho Tự động, 0 cho Thủ công
        document.getElementById("toggleText").innerText = value === 0 ? "CHẾ ĐỘ THỦ CÔNG" : "CHẾ ĐỘ TỰ ĐỘNG";
        sendCommand("chedo", value); // Gửi với key 'chedo'
    }
</script>
<body onload="updatedata()">
    <div class="container">
        <h1 class="ten">HỆ THỐNG KIỂM SOÁT ĐÈN GIAO THÔNG</h1>
        <div class="traffic-light traffic-light1">
            <div class="red-light" id="led1"></div>
            <div class="yellow-light" id="led2"></div>
            <div class="green-light" id="led3"></div>    
        </div>
        <div class="thoigian thoigian1">
            <label id="VL1">99</label>
        </div>
        <div class="traffic-light traffic-light2">
            <div class="red-light" id="led4"></div>
            <div class="yellow-light" id="led5"></div>
            <div class="green-light" id="led6"></div>
        </div>
        <div class="thoigian thoigian2">
            <label id="VL2">99</label>
        </div>
        <div class="chuki">
            <h1>CHU KÌ: <label id="TONG">0</label></h1>
        </div>
        <div class="nhapgt">
            <div class="caidat-label">Cài chu kỳ sáng đèn:</div>
            <div class="input-group">
                <input class="onhap4" id="caidat4" style="font-size: 30px" placeholder="Nhập giá trị vào đây">
                <button id="myBtn4" class="annut4" onclick="caidatChuKy()" style="font-size: 20px">Gửi</button>
            </div>
            <div class="toggle-switch">
                <input type="checkbox" id="myToggle" onchange="toggleSwitch()">
                <label for="myToggle"></label>
                <span class="trangthai" id="toggleText">CHẾ ĐỘ THỦ CÔNG</span>
            </div>
            <div class="TT">
            <h1>TRẠNG THÁI:<label id="TT">BÌNH THƯỜNG</label></h1>
        </div>
        </div>
    </div>
</body>
</html>
