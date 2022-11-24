# 网站文件
共享开源文件夹

石头剪刀布小游戏源代码一览：
# 运行须知：
# 1.必须将PY版本更换成3.7.7（别问我怎么知道的）
# 2.必须将PY插件（运行库）protobuf版本更换为3.20.0（别问我怎么知道的）
# 3.运行后1小时5秒未操作自动结束进程（太懒了就重根源解决了问题...反正程序能跑就是了！！！）
# 4.本程序改良于YouTube @ Murtaza's_Workshop-Robotics_and_AI 也有功能上的更新（要尊重原作者！！！）
# 5.本代码是我呕心沥血...额...费尽心血写的希望给本作者BiliBili@ 我系小麦 一个三连[2币]（就比如一堆错误要一点点改本来两天就做好了，清理了下垃圾就不能运行了，所以我增加了运行须知前两点）
# 6.按下'S'以开始游戏，按下'r'以重启游戏，按下'e'以结束游戏
# 7.按下'S'后从3秒后开始游戏，分数在方框下方
# 8.按下'S'后未计时就再多按几次可能会有延迟，游戏时间不限，主要以娱乐为主
# 9.本已代码开源（下载地址：https://github.com/Mr-Bo-github/website/tree/石头剪刀布小游戏）
# 10.下面就是正式程序了（！！！如果运行不了请看一下运行须知别BB！！！）
# 导入插件
import random
import cv2
from cvzone.HandTrackingModule import HandDetector
import time
# 设置视频（摄像头）
cap = cv2.VideoCapture(0)
gege = cv2.VideoCapture(f'zy/0.mp4')
# 不同设备（摄像头）设置统一视频显示大小
cap.set(3, 640)
cap.set(4, 480)
# 识别手数量最大值
detector = HandDetector(maxHands=1)
# 定义（初始化）变量
timer = 0
stateResult = False
startGame = False
gegeztbf = 0
# AI分数，玩家分数
scores = [0, 0]
# 主程序
while True:
    # 背景将文件导入
    imgBG = cv2.imread("zy/BG.png")
    # 读取视频
    success, img = cap.read()
    # 读取视频
    lookgege, gegeimg = gege.read()
    # 缩放
    imgScaled = cv2.resize(img, (0, 0), None, 0.908, 0.908)
    # 裁剪
    imgScaled = imgScaled[:, 218:480]
    # 缩放
    imgScaled1 = cv2.resize(gegeimg, (0, 0), None, 0.908, 0.908)
    # 裁剪
    imgScaled1 = imgScaled1[:, 218:480]
    # 原创声明（右上角文本）
    cv2.putText(imgBG, "@ Originated_by_Mr_Bo", (1070, 15), cv2.FONT_HERSHEY_PLAIN, 1, (0, 0, 0), 3)
    cv2.putText(imgBG, "@ Originated_by_Mr_Bo", (1070, 15), cv2.FONT_HERSHEY_PLAIN, 1, (255, 255, 255), 1)
    # 手部识别
    hands, img = detector.findHands(imgScaled)
    # 游戏部分
    if startGame:
        # 游戏状态判断（倒计时）
        if stateResult is False:
            timer = time.time() - initialTime
            cv2.putText(imgBG, str(int(timer)), (600, 350), cv2.FONT_HERSHEY_PLAIN, 6, (0, 0, 255), 4)
            # 计时判断
            if timer > 3:
                stateResult = True
                # 重置时间
                timer = 0
                # 手指识别
                if hands:
                    # 初始化
                    playerMove = None
                    # 设置（初始化）列表（手部）
                    hand = hands[0]
                    # 识别（竖起）的手指并记录在列表中
                    fingers = detector.fingersUp(hand)
                    # 石头
                    if fingers == [0, 0, 0, 0, 0]:
                        playerMove = 1
                    # 丝绸
                    if fingers == [1, 1, 1, 1, 1]:
                        playerMove = 2
                    # 剪刀
                    if fingers == [0, 1, 1, 0, 0]:
                        playerMove = 3
                    # AI部分
                    # 让AI从石头剪刀布（1，2，3）中抽一个
                    randomNumber = random.randint(1, 3)
                    # imgAI = cv2.imread(f'zy/{randomNumber}.png', cv2.IMREAD_UNCHANGED)
                    # 总是报错滚一边去！！！
                    # imgBG = cvzone.overlayPNG(imgBG, imgAI, (85, 851))
                    # 于是...我想了一个更好的注意~就是把我家割割弄过来，让使用者感觉处处都有那个TA~
                    # 显示石头剪刀布（1，2，3）
                    gege = cv2.VideoCapture(f'zy/{randomNumber}.mp4')
                    # 读取
                    lookgege, gegeimg = gege.read()
                    # 缩放
                    imgScaled1 = cv2.resize(gegeimg, (0, 0), None, 0.908, 0.908)
                    # 裁剪
                    imgScaled1 = imgScaled1[:, 218:480]
                    # 玩家胜利互动
                    if (playerMove == 1 and randomNumber == 3) or \
                            (playerMove == 2 and randomNumber == 1) or \
                            (playerMove == 3 and randomNumber == 2):
                        # 太复杂了，还是随机好
                        # if int(scores[1]) == 1:
                            # gegezt = cv2.VideoCapture(f'kunkun/2.mp4')
                        # if int(scores[1]) == 2:
                            # gegezt = cv2.VideoCapture(f'kunkun/3.mp4')
                        # if int(scores[1]) == 3:
                            # gegezt = cv2.VideoCapture(f'kunkun/4.mp4')
                        # if int(scores[1]) == 4:
                            # gegezt = cv2.VideoCapture(f'kunkun/5.mp4')
                        # if int(scores[1]) >= 5:
                            # gegezt = cv2.VideoCapture(f'kunkun/{gegeztsj}.mp4')
                        # 随机互动视频从视频（1~5）抽一个
                        gegeztsj = random.randint(2, 5)
                        # 设置播放视频
                        gegezt = cv2.VideoCapture(f'kunkun/{gegeztsj}.mp4')
                        # 防报错（判定是否设置视频）
                        gegeztbf = 1
                    # 玩家失败互动
                    elif (playerMove == 3 and randomNumber == 1) or \
                            (playerMove == 1 and randomNumber == 2) or \
                            (playerMove == 2 and randomNumber == 3):
                        # 设置播放视频
                        gegezt = cv2.VideoCapture(f'kunkun/1.mp4')
                        # 防报错（判定是否设置视频）
                        gegeztbf = 1
                    # 纯属强迫症
                    else:
                        # 设置播放视频
                        gegezt = cv2.VideoCapture(f'kunkun/0.mp4')
                        # 防报错（判定是否设置视频）
                        gegeztbf = 0
                    # 显示互动视频
                    while gegeztbf == 1:
                        # 读取视频
                        lookgegezt, gegeztimg = gegezt.read()
                        # 如果视频正常播放
                        if lookgegezt:
                            # 缩放视频
                            imgScaled2 = cv2.resize(gegeztimg, (0, 0), None, 0.908, 0.908)
                            # imgScaled2 = imgScaled2[:, 218:480]
                            # imgBG[86:522, 167:429] = imgScaled2
                            # 显示窗口
                            cv2.imshow('gegezt', imgScaled2)
                            # 延迟（防止视频播放太快）
                            cv2.waitKey(10)
                        # 视频播放结束（视频播放不正常）
                        else:
                            # 关闭窗口
                            cv2.destroyWindow('gegezt')
                            # 将是否设置视频更改为0（未设置）
                            gegeztbf = 0
                            # 退出循环
                            break

                    # 玩家加分
                    if (playerMove == 1 and randomNumber == 3) or \
                            (playerMove == 2 and randomNumber == 1) or \
                            (playerMove == 3 and randomNumber == 2):
                        # 在变量（玩家）中增加1分
                        scores[1] += 1
                    # AI加分
                    if (playerMove == 3 and randomNumber == 1) or \
                            (playerMove == 1 and randomNumber == 2) or \
                            (playerMove == 2 and randomNumber == 3):
                        # 在变量（AI）中增加1分
                        scores[0] += 1
                    # 检查（输出玩家与AI的游戏角色）
                    print("手指：", fingers, "判断：", playerMove, "AI：", randomNumber)
    # 视频显示位置
    imgBG[86:522, 851:1113] = imgScaled
    imgBG[86:522, 167:429] = imgScaled1
    # if stateResult:
    # imgBG = cvzone.overlayPNG(imgBG, imgAI, (85, 851))
    # VS分数显示
    cv2.putText(imgBG, str(scores[0]), (170, 560), cv2.FONT_HERSHEY_PLAIN, 3, (255, 255, 255), 6)
    cv2.putText(imgBG, str(scores[1]), (855, 560), cv2.FONT_HERSHEY_PLAIN, 3, (255, 255, 255), 6)
    # 设置摄像头
    # success, img = cap.read()
    # 显示窗口
    # cv2.imshow("Image", img)
    cv2.imshow("BG", imgBG)
    # cv2.imshow("Scaled", imgScaled)
    # 按键判断
    key = cv2.waitKey(1)
    # 开始游戏
    if key == ord('s'):
        startGame = True
        initialTime = time.time()
        stateResult = False
    # 重启游戏
    elif key == ord('r'):
        scores = [0, 0]
        gege = cv2.VideoCapture(f'zy/0.mp4')
    # 结束游戏
    elif key == ord('e'):
        cv2.destroyAllWindows()
        break
    # 延迟
    else:
        cv2.waitKey(1)
