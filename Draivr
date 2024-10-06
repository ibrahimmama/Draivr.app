<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>استقبال طلبات</title>
</head>
<body>
    <h1 style="text-align: center;">استقبال طلبات الزبائن</h1>
    <button id="getRequest" style="display: block; margin: 0 auto;">استقبال طلب جديد</button>
    <p id="output" style="text-align: center;"></p>

    <script src="https://www.gstatic.com/firebasejs/9.1.2/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.1.2/firebase-database.js"></script>
    <script>
        // تكوين Firebase
        const firebaseConfig = {
            apiKey: "AIzaSyCow0kJbcJ7OUzaHOBqXp1hF1LPSxb6dBo",
            authDomain: "alnashme-tawsel.firebaseapp.com",
            databaseURL: "https://alnashme-tawsel-default-rtdb.firebaseio.com",
            projectId: "alnashme-tawsel",
            storageBucket: "gs://alnashme-tawsel.appspot.com",
            messagingSenderId: "76863416572",
            appId: "1:76863416572:android:e75569b3ef02142baf8f79"
        };

        // تهيئة Firebase
        const app = firebase.initializeApp(firebaseConfig);
        const database = firebase.database();

        document.getElementById('getRequest').addEventListener('click', function() {
            // استرجاع طلبات الزبائن من Firebase
            firebase.database().ref('requests').orderByChild('status').equalTo('pending').limitToFirst(1).on('value', function(snapshot) {
                snapshot.forEach(function(childSnapshot) {
                    const data = childSnapshot.val();
                    const customerLat = data.customerLocation.latitude;
                    const customerLng = data.customerLocation.longitude;

                    // فتح تطبيق الخرائط لتوجيه السائق إلى الزبون
                    const url = `https://www.google.com/maps/dir/?api=1&destination=${customerLat},${customerLng}&travelmode=driving`;
                    window.open(url, '_blank');

                    // تحديث حالة الطلب إلى "مقبول"
                    firebase.database().ref('requests/' + childSnapshot.key).update({
                        status: 'accepted'
                    });

                    document.getElementById('output').innerText = 'تم قبول الطلب، جاري التوجيه...';
                });
            });
        });
    </script>
</body>
</html>
