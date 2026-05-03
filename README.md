import subprocess
import hashlib
import time
def run(cmd):
    try:
        out = subprocess.check_output(cmd, shell=True, stderr=subprocess.DEVNULL)
        return out.decode().strip()
    except Exception:
        return ""

android_id = run("settings get secure android_id")
serial = run("getprop ro.serialno") or run("getprop ro.boot.serialno") or run("getprop ro.hardware")
brand = run("getprop ro.product.brand")
model = run("getprop ro.product.model")
mac = run("cat /sys/class/net/wlan0/address 2>/dev/null")
values = [v for v in [android_id, serial, brand, model, mac] if v]
concat = "|".join(values)

SALT = "سِرّ_خاص_قوي_غير_مُشارَك"

full = SALT + "|" + concat
h = hashlib.sha256(full.encode()).hexdigest()
hash=['294b6221ca2add3f64f9d583b20bce571fc61daf1acb85687b4d73342d1b6c53','59133419746d7da1e3e3bb1382299c823bd79a66fca3b45bf07d351c5df5680a','22c774cafc84765480eeabf68cff63ea5de7bf9a08c630a80e8ac8bcea77d971','21be8f906a15d50043152b0d698e00eb3b0931f5b10b47c27056c682101a85b5','5492156e8956344a4cfd3ec430368d2d85a4c8fca36ce8a4ca7e2f30f6eb25b0','9b8f00e0e36b78821568aa4159f548333f00ce0f5c6ae618b7a87e0417ed49c6','2f6c72b6e343b52fd0150a61a4c8cbaad234e5fe1aa644572491433682ccfa7b','eef2946c43b40d0d75e502abe6ce73142fe1bb675a663b2b63fbccc63e6b5726','a771d27484bf2eda1917894265f80cbdab1d7b2e49a47042f509a6d7497279e2']
if h in hash:
    print('good / هاتفك مصرح للدخول ')
    pass
else :
	while True:
	   print('your code is /', h)
	   print()
	   print('للتفعيل راسل المطور وادفع حق التحديث 1 usdt او 2k رشق وبعدها ارسله الكود يفعل لك ملاحضة لا تدور مجاني . ماراح ارد عليك')
	   time.sleep(90)
     
