

<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <title>جلسات البدو - تعاونية لعميرة</title>
  <script src="https://sdk.minepi.com/pi-sdk.js"></script>
  <style>
    body { font-family: 'Cairo', sans-serif; background: #f8f1e4; margin: 0; padding: 20px; }
    header { background: #a0522d; color: white; padding: 20px; border-radius: 10px; text-align: center; }
    section { margin-top: 20px; padding: 20px; background: white; border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    h2 { color: #a0522d; }
    .btn { background: #d2691e; color: white; border: none; padding: 10px 20px; border-radius: 5px; cursor: pointer; }
    .btn:hover { background: #b45e14; }
  </style>
</head>
<body>

  <header>
    <h1>جلسات البدو - تعاونية لعميرة</h1>
    <p>تجربة بدوية أصيلة مع الشاي والموسيقى الصحراوية</p>
  </header>

  <section>
    <h2>الخدمة</h2>
    <p>جلسة بدوية لمدة ساعتين تشمل:</p>
    <ul>
      <li>خيمة تقليدية</li>
      <li>شاي صحراوي</li>
      <li>ألعاب بدوية (سيك، سبع حجار...)</li>
      <li>موسيقى من التراث الحساني</li>
    </ul>
    <p><strong>السعر:</strong> 3 Pi لكل شخص</p>
    <button class="btn" onclick="payWithPi()">احجز الآن وادفع بـ Pi</button>
  </section>

  <section>
    <h2>تواصل معنا</h2>
    <p><strong>الموقع:</strong> جماعة طاح - منطقة لعميرة</p>
    <p><strong>الهاتف:</strong> 0658041944</p>
    <p><strong>البريد:</strong> laamiracoop@gmail.com</p>
  </section>

  <script>
    const payment = {
      amount: 3,
      memo: "جلسة بدوية",
      metadata: { service: "جلسة بدوية" }
    };

    async function payWithPi() {
      Pi.init({
        version: "2.0",
        sandbox: true, // احذفها في الإنتاج الحقيقي
        onReady: () => {
          Pi.createPayment(payment, {
            onReadyForServerApproval: function(paymentId) {
              console.log("طلب موافقة الخادم", paymentId);
              // هنا يمكن إرسال paymentId إلى الخادم الخاص بك للموافقة
            },
            onReadyForServerCompletion: function(paymentId, txid) {
              alert("تم الحجز بنجاح! رقم المعاملة: " + txid);
            },
            onCancel: function(paymentId) {
              alert("تم إلغاء العملية.");
            },
            onError: function(error) {
              alert("حدث خطأ: " + error.message);
            }
          });
        }
      });
    }
  </script>

</body>
</html>

