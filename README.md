import os
import shutil
import time

TARGET_DIRS = [
    '/var/log',
    '/tmp',
    './downloads/icons',
    './app/cache'
]

DAYS_TO_KEEP = 30
SECONDS_IN_DAY = 86400
EXPIRATION_TIME = time.time() - (DAYS_TO_KEEP * SECONDS_IN_DAY)

def cleanup():
    for target in TARGET_DIRS:
        if not os.path.exists(target):
            continue
            
        for root, dirs, files in os.walk(target):
            for name in files:
                file_path = os.path.join(root, name)
                try:
                    if os.path.getmtime(file_path) < EXPIRATION_TIME:
                        os.remove(file_path)
                        print(f"[DELETED] {file_path}")
                except Exception as e:
                    print(f"[ERROR] {file_path}: {e}")

            for name in dirs:
                dir_path = os.path.join(root, name)
                try:
                    if not os.listdir(dir_path) and os.path.getmtime(dir_path) < EXPIRATION_TIME:
                        os.rmdir(dir_path)
                        print(f"[REMOVED DIR] {dir_path}")
                except Exception as e:
                    print(f"[ERROR DIR] {dir_path}: {e}")

if name == "main":
    cleanup()




BY AKUZE 8 klass kod dlya othsiski kewa v servere mechta DEV OPS inzhener