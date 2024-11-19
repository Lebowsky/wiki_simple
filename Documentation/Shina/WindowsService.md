---
title: WindowsService
description: 
published: true
date: 2024-11-19T13:18:39.475Z
tags: 
editor: markdown
dateCreated: 2024-11-19T13:18:39.475Z
---

# Windows служба
```python
import servicemanager
import win32service
import win32serviceutil
import win32event
import threading
import os
import sys
import subprocess


class SimpleBusService(win32serviceutil.ServiceFramework):
    _svc_name_ = "SimpleBusService"
    _svc_display_name_ = "Simple Bus Service"
    _svc_description_ = "Служба для запуска SimpleBus"

    def __init__(self, args):
        win32serviceutil.ServiceFramework.__init__(self, args)
        self.hWaitStop = win32event.CreateEvent(None, 0, 0, None)
        self.running = True

    def SvcStop(self):
        self.ReportServiceStatus(win32service.SERVICE_STOP_PENDING)
        self.running = False
        win32event.SetEvent(self.hWaitStop)

    def SvcDoRun(self):
        servicemanager.LogInfoMsg("SimpleBusService: Старт сервиса...")

        try:
            # Запуск основного процесса в отдельном потоке
            thread = threading.Thread(target=self.run_script)
            thread.start()

            # Ожидание команды остановки
            while self.running:
                win32event.WaitForSingleObject(self.hWaitStop, 5000)
        except Exception as e:
            servicemanager.LogErrorMsg(f"SimpleBusService: Ошибка SvcDoRun: {str(e)}")

        servicemanager.LogInfoMsg("SimpleBusService: Сервис остановился.")


    def run_script(self):
        try:
            # Путь к скрипту
            script_path = os.path.join(os.path.dirname(__file__), "simplebus.py")

            # Проверяем, существует ли файл
            if not os.path.exists(script_path):
                raise FileNotFoundError(f"Script file not found: {script_path}")

            # Запускаем процесс
            servicemanager.LogInfoMsg(f"SimpleBusService: Старт сервиса {script_path}")
            process = subprocess.Popen([sys.executable, script_path], shell=False)

            # Ожидание завершения процесса
            process.wait()
        except Exception as e:
            servicemanager.LogErrorMsg(f"SimpleBusService: Ошбка пока работал сервис: {str(e)}")


if __name__ == "__main__":
    if '--debug' in sys.argv:
        import time

        class DebugSimpleBusService:
            def __init__(self):
                self.running = True

            def SvcDoRun(self):
                print("SimpleBusService: Запустили дебаг.")
                try:
                    self.run_script()
                except Exception as e:
                    print(f"SimpleBusService: Ошибка в дебаге: {e}")
                finally:
                    print("SimpleBusService: Дебаг остановился.")

            def run_script(self):
                # Логика основного процесса
                script_path = os.path.join(os.path.dirname(__file__), "simplebus.py")
                if not os.path.exists(script_path):
                    raise FileNotFoundError(f"Не найден скрипт: {script_path}")
                print(f"Запуск скрипта: {script_path}")
                process = subprocess.Popen([sys.executable, script_path], shell=False)
                process.wait()

        # Режим отладки
        service = DebugSimpleBusService()
        try:
            service.SvcDoRun()
        except KeyboardInterrupt:
            print("SimpleBusService: Interrupted by user.")
    else:
        # Если запущен обычный режим, обрабатываем аргументы
        if len(sys.argv) > 1:
            win32serviceutil.HandleCommandLine(SimpleBusService)
        else:
            # Подготовка и запуск службы
            servicemanager.Initialize()
            servicemanager.PrepareToHostSingle(SimpleBusService)
            servicemanager.StartServiceCtrlDispatcher()
```