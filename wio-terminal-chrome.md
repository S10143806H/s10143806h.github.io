<h1> 用 Wio Terminal 打造體感 Chrome 恐龍游戲 </h1>


* [原文轉載自](https://makergram.com/blog/play-chromes-dino-game-physically/)

:::info
在這個項目中，我們將結合 "機器學習" 和 "Wio Terminal" ，親身體驗“體感” chrome 恐龍遊戲。
:::

## 介紹

由於新冠疫情第二波全球大流行，我一直呆在家裡沒有做太多的體育活動，上個月我得了胃病，在諮詢了醫生收，他建議我進行少量的體育活動，可以幫助我避免再次這些問題。

我嘗試使用一個移動應用程序，幫助在沒有設備的情況下進行體育活動，我還邀請了我的小侄子和我一起鍛煉，但他們不感興趣。

然後我就想到設計這個項目，可以有趣地幫助我們燃燒一些卡路里，使我們在新冠疫情期間保持健康。🤗

## 怎麼玩的？

1. 將 Wio 終端連接到電腦
2. 打開 Dino chrome://dino/
3. 連接 Wio 終端
4. 跳躍🙌

## 它是如何運作的

1. 把 Wio Terminal (由Seeed Studio研製）放在口袋裏，它運行基於 Edge Impluse 的 TinyML 的機器學習模型進行用戶動作的推理
2. 例如：當用戶（模仿游戲中小恐龍）跳躍的時候， Wio Terminal 內置的加速度計可以讀出數據，將這些數據傳遞到 Edge Impluse，基於算法判斷用戶當時的動作：
    - 跳躍 
    - 靜止
4. 如果檢測到當時用戶在做“跳躍”的動作，Wio Terminal 會通過 HID 接口模擬按下鍵盤的“空格鍵”，并且發送到計算機。

![](https://i.imgur.com/2p4ixky.png)


## 上手指南

首先，致謝 Edge Impulse Studio 這個小型的機器學習平臺，同時也感謝 Wio Terminal， 兩者的合并使我的項目想法更容易實現。因爲這個，項目是機器學習和嵌入式電子產品的結合，下面我將逐步解釋以讓這個項目，這樣的話你也可以自己動手實現。

![](https://i.imgur.com/xiLijhd.png)

首先，我們需要收集數據，然後我們需要用特定的 “機器學習算法” 訓練數據集，之後，我們將創建一個 ***Impulse***。通過這個 Impulse，我們將提取 ***特徵*** 並創建一個 ***判斷模型***，最後，我們將推理模型加載到 Wio Terminal， 將模型沒有遇到的數據（也可以成爲新的數據，或是測試數據）並通過模型進行 ***分類***。

:::success
下面 Salman 會爲我們帶來將進行 **“十分詳細”** 的解釋説明
:::


### 第 1 步：數據收集 📚

機器學習項目的第一步，是要收集足夠的數據並創建 “訓練集”，在這個專案中，我們的數據來自 Wio Terminal 的加速度計的讀數。雖然數據收集是一項有點乏味的工作，但是 Edge Impluse 將一切變得很輕鬆。

#### 1.1：創建 [Edge Impluse](https://studio.edgeimpulse.com/login) 帳戶

首先，我們需要創建一個邊緣脈沖帳戶，或者如果您已有帳戶，請輸入用戶名/電子郵件和密碼。

![](https://i.imgur.com/vkIxJBE.png =500x250)

#### 1.2：創建邊緣

Impulse項目創建帳戶後，我們需要創建一個 edgeImpulse 項目。對於點擊您的個人資料，並選擇創建一個新的項目或使用該網址


然後提供項目名稱，然後單擊創建新項目
<!-- 

接下來就可以看到studio頁面了，說明你成功創建了一個edge Impulse項目🎉


### 1.3：在此處連接 Wio 終端

我們使用 SeeedStudio Wio 終端作為我們的邊緣設備來收集數據集和推理機器學習模型。

Seeed Wio 終端是 Seeed Studios 的開發板，帶有 Cortex-M4 微控制器、運動傳感器、LCD 顯示器和 Grove 連接器，可輕鬆連接外部傳感器。Seeed Studio 已將對該開發板的支持添加到 Edge Impulse，因此您可以從該工作室對原始數據進行採樣並構建機器學習模型。該板可直接從Seeed以 29 美元的價格購買。

您可以在此處的Wio Terminal Edge Impulse Getting Started 中找到來自 Seeed studio 的出色指南，解釋如何將邊緣脈衝與 Wio 終端一起使用。無論如何，我將概述如何連接 Wio 終端。

步驟 1.2.1：上傳 EdgeImpulse UF2 固件

將 Wio 終端連接到您的計算機。通過快速滑動電源開關兩次進入引導加載程序模式。


名為 Arduino 的外部驅動器應出現在您的 PC 上。將下載的Edge Impulse uf2 固件文件拖到 Arduino 驅動器中。現在，Edge Impulse 已加載到 Seeeduino Wio 終端上！

步驟 1.2.2：使用 WebUSB 連接 Wio 終端

選擇使用 WebUSB 連接


選擇 Wio 終端端口並點擊連接。


連接成功🎉


步驟 1.3：開始 收集日期

要收集數據，我們需要選擇正確的傳感器、標記數據、提供以毫秒為單位的樣本長度並提供傳入數據的頻率。右邊是參數，你可以看到標籤是跳轉，所以我需要記錄傳感器參數的跳轉數據。


在點擊採樣之後，由於我們提供了 10000 毫秒作為採樣長度，它將以 10 秒內置加速度計數據開始。


因此，採樣時將 Wio 終端連接到您的身體並跳躍10 秒鐘。


採集完成後，可以看到原始數據和样品列表


像這樣，我們需要收集 Jump 和 Idle 原始數據的 18 個樣本。（數據越多越好，並嘗試均衡所有數據集，否則模型將欠擬合或過擬合）


我們現在已經成功收集到原始數據🎉

第 2 步：拆分訓練和測試數據集 ✂️
為了構建更好的 ML 模型，我們需要提供質量數據並測試模型的質量，我們需要規模，用相同的訓練數據測試模型是不好的，所以為了衡量模型的準確性，我們需要隨機原始來自收集的數據集的數據並將其標記為測試數據並與訓練數據隔離，最後在建模完成時，我們使用此測試數據集來衡量模型的準確性。

訓練集：您可以提取特徵並訓練以適應模型等。

測試集：通過預測數據集來衡量模型的準確性。

在Edge Impluse studio 中， 我們可以輕鬆地將數據隨機拆分為訓練和測試數據集。轉到項目儀表板並單擊重新平衡數據集


您會收到一條警告消息，如果您覺得沒問題，請重新平衡


現在您可以看到測試數據


如果不平衡，您可以手動移動每個數據集。

----

### 第二步：脈衝設計✨

脈衝取原始數據，切片它在較小的窗口，使用小號ignal處理塊到特徵提取，然後使用一個學習塊來進行分類的新數據。信號處理模塊始終為相同的輸入返回相同的值，用於使原始數據更易於處理，而學習模塊則從過去的經驗中學習。在我們的脈衝設計中，我們需要注意三個步驟

創建脈衝 - 選擇數據系列、處理塊、學習塊和輸出特徵
選擇和構建處理模塊（光譜特徵）
選擇和構建學習塊（神經網絡分類器）

#### 步驟 2.1：創建衝動

首先，我們需要選擇數據系列 中的窗口大小等參數，處理塊和學習塊Finlay 選擇輸出特徵，即標籤。


在這個項目中，我使用Window size 1000 ms 和Spectral Analysis作為處理塊，因為它非常適合分析重複運動，例如來自加速度計的數據。隨著時間的推移提取信號的頻率和功率特性，對於學習塊， 我選擇了神經網絡 (Keras)用於從數據中學習模式並將其應用於新數據。非常適合對運動進行分類或識別音頻。

#### 步驟 2.1：構建處理模塊- 頻譜分析


在我們的項目中，我們使用頻譜分析作為處理塊，因為它非常適合分析重複運動，例如來自加速度計的數據。要配置您的信號處理模塊，請單擊左側菜單中的Spectral features。這將在屏幕頂部顯示原始數據（您可以通過下拉菜單選擇其他文件），以及通過右側圖形顯示信號處理的結果。對於光譜特徵塊，您將看到以下圖表：

濾波後 - 應用低通濾波器後的信號。這將消除噪音。
頻域 - 信號重複的頻率（例如，每秒進行一次波浪運動將在 1 Hz 處顯示峰值）。
頻譜功率 - 在每個頻率進入信號的功率量。

一個好的信號處理模塊會對相似的數據產生相似的結果。如果您四處移動滑動窗口（在原始數據圖表上），圖表應該保持相似。此外，當您切換到具有相同標籤的另一個文件時，您應該會看到類似的圖形，即使設備的方向不同。


對結果感到滿意後，單擊Save parameters。這會將您發送到“功能生成”屏幕。在這裡，您將：

在窗口中拆分所有原始數據（基於窗口大小和窗口增加）。
在所有這些窗口上應用光譜特徵塊。

單擊生成特徵以開始該過程。


#### 步驟 2.3：選擇並構建學習塊（神經網絡分類器）/配置神經網絡

處理完所有數據後，就可以開始訓練神經網絡了。神經網絡是一組算法，鬆散地模仿人腦，旨在識別模式。我們在這裡訓練的網絡將信號處理數據作為輸入，並嘗試將其映射到四個類之一。


有了這個神經網絡架構，我開始了訓練。如果我們願意，我們可以添加更多額外的密集層。


一旦我們點擊Start Training，根據訓練週期的  數量，訓練神經網絡將花費那麼多的 epoch。

一個時期是指整個訓練數據集的一個循環
訓練完成後，我們可以看到模型訓練的性能。


在這裡我們得到了非常好的性能結果，因為它只有兩個標籤。

---

### 第三步：  直播分類🔍。

從前面的訓練部分我們知道我們的模型將如何執行，但是網絡在新數據上的表現如何？單擊菜單中的實時分類進行查找。


連接設備並單擊開始採樣，或者您可以從前面的列表中選擇一個簡單的。


您可以看到實時分類結果。從 10 秒開始，它發現 107 Jump nd 5 為 Idle 和一個不確定的運動，這意味著它無法描述。


我們還可以在實時樣本所在的圖表中看到它們，並查看訓練數據和分類數據。

### 第 4 步：  測試數據分類🧪。

在第一個數據收集部分，我們實際上選擇了一些數據樣本作為測試數據，以查看我們的模型性能。在模型測試選項卡中，單擊全部分類以開始分類。


您可以看到模式測試非常準確。


### 第 5 步：模型部署✔️。

我們可以通過不同的方式下載 Impulse 模型。


由於我們有 Wio 終端，我選擇了Arduino 庫。


該EON可以使神經網絡在高達55％較少的內存，並減少35％ROMEON通過編譯你的神經網絡的C ++源代碼實現了它的魔力。這與其他嵌入式神經網絡運行時不同，例如用於微控制器的 TensorFlow Lite，後者俱有通用解釋器，然後在運行時加載您的模型。通過將神經網絡編譯為源代碼，您不需要解釋器，可以更輕鬆地將數據轉移到 ROM 中，並且鏈接器確切地知道正在使用哪些操作，從而能夠消除更多代碼。您可以在此處閱讀更多信息：https : //www.edgeimpulse.com/blog/introducing-eon


單擊構建後，模型在後台構​​建，完成後會自動下載。

步驟 5.1 安裝 Arduino 庫

通過 Arduino IDE 添加此庫：Sketch > Include Library > Add .ZIP Library...然後可以在以下位置找到示例：文件 > 示例 > seeed-wioTerminal_inferencing。


步驟 5.2 將示例草圖上傳到 Wio 終端

選擇正確的端口和闆卡，然後點擊上傳。


上傳草圖後，它立即開始採樣和推理。您可以打開串行監視器查看結果。


### 第 6 步：添加鍵盤庫來玩 Dino 遊戲🎮

現在我們構建了一個嵌入式設備，可以讀取加速度計數據並預測跳躍或空閒。為了玩恐龍遊戲，我們只需要發送一個可以是空格鍵或回車鍵的擊鍵，這樣我們就可以在一個人跳躍並完成項目時用 Wio 終端模擬該擊鍵。

我使用了 Arduino 的鍵盤庫，該庫允許具有 USB 功能的 Arduino 板充當鍵盤。我通過添加條件修改了代碼。

if (result.classification[1].value > 0) {
Serial.println("Jumped...................");
Keyboard.write(KEY_UP_ARROW);
delay(100);
}

#### 完整代碼

``` CPP
/* Includes ---------------------------------------------------------------- */
#include <seeed-wioterminal_inference.h>
#include"LIS3DHTR.h"
LIS3DHTR<TwoWire> lis;
#include "Keyboard.h" //keyboard library

/* Constant defines -------------------------------------------------------- */
#define CONVERT_G_TO_MS2    9.80665f

/* Private variables ------------------------------------------------------- */
static bool debug_nn = false; // Set this to true to see e.g. features generated from the raw signal

/**
  @brief      Arduino setup function
*/
void setup()
{
  // put your setup code here, to run once:
  Serial.begin(115200);
  while (!Serial) {
  }
  Serial.println("Edge Impulse Inferencing Demo");

  lis.begin(Wire1);

  if (!lis.available()) {
    ei_printf("Failed to initialize IMU!\r\n");
    while (1);
  }
  else {
    ei_printf("IMU initialized\r\n");
  }

  lis.setOutputDataRate(LIS3DHTR_DATARATE_100HZ); // Setting output data rage to 25Hz, can be set up tp 5kHz
  lis.setFullScaleRange(LIS3DHTR_RANGE_16G); // Setting scale range to 2g, select from 2,4,8,16g

  if (EI_CLASSIFIER_RAW_SAMPLES_PER_FRAME != 3) {
    ei_printf("ERR: EI_CLASSIFIER_RAW_SAMPLES_PER_FRAME should be equal to 3 (the 3 sensor axes)\n");
    return;
  }
}

/**
  @brief      Printf function uses vsnprintf and output using Arduino Serial

  @param[in]  format     Variable argument list
*/
void ei_printf(const char *format, ...) {
  static char print_buf[1024] = { 0 };

  va_list args;
  va_start(args, format);
  int r = vsnprintf(print_buf, sizeof(print_buf), format, args);
  va_end(args);

  if (r > 0) {
    Serial.write(print_buf);
  }
}

/**
  @brief      Get data and run inferencing

  @param[in]  debug  Get debug info if true
*/
void loop()
{
  ei_printf("Sampling...\n");

  // Allocate a buffer here for the values we'll read from the IMU
  float buffer[EI_CLASSIFIER_DSP_INPUT_FRAME_SIZE] = {0};

  for (size_t ix = 0; ix < EI_CLASSIFIER_DSP_INPUT_FRAME_SIZE; ix += 3) {
    // Determine the next tick (and then sleep later)
    uint64_t next_tick = micros() + (EI_CLASSIFIER_INTERVAL_MS * 1000);

    lis.getAcceleration(&buffer[ix], &buffer[ix + 1], &buffer[ix + 2]);

    buffer[ix + 0] *= CONVERT_G_TO_MS2;
    buffer[ix + 1] *= CONVERT_G_TO_MS2;
    buffer[ix + 2] *= CONVERT_G_TO_MS2;

    delayMicroseconds(next_tick - micros());
  }

  // Turn the raw buffer in a signal which we can the classify
  signal_t signal;
  int err = numpy::signal_from_buffer(buffer, EI_CLASSIFIER_DSP_INPUT_FRAME_SIZE, &signal);
  if (err != 0) {
    ei_printf("Failed to create signal from buffer (%d)\n", err);
    return;
  }

  // Run the classifier
  ei_impulse_result_t result = { 0 };

  err = run_classifier(&signal, &result, debug_nn);
  if (err != EI_IMPULSE_OK) {
    ei_printf("ERR: Failed to run classifier (%d)\n", err);
    return;
  }

  // print the predictions
  ei_printf("Predictions ");
  ei_printf("(DSP: %d ms., Classification: %d ms., Anomaly: %d ms.)",
            result.timing.dsp, result.timing.classification, result.timing.anomaly);
  ei_printf(": \n");
  for (size_t ix = 0; ix < EI_CLASSIFIER_LABEL_COUNT; ix++) {
    ei_printf("    %s: %.5f\n", result.classification[ix].label, result.classification[ix].value);

    if (result.classification[1].value > 0) {
      Serial.println("Jumped...................");
      Keyboard.write(KEY_UP_ARROW);
     delay(100);
      
    }



  }
#if EI_CLASSIFIER_HAS_ANOMALY == 1
  ei_printf("    anomaly score: %.3f\n", result.anomaly);
#endif
}

#if !defined(EI_CLASSIFIER_SENSOR) || EI_CLASSIFIER_SENSOR != EI_CLASSIFIER_SENSOR_ACCELEROMETER
#error "Invalid model for current sensor"
#endif
```

### 第 7 步：最終測試 🚀

現在我們完成了所有事情，

打開 Dino chrome://dino/
連接 Wio 終端
跳躍🙌
 -->
