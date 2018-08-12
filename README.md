# Havven模拟器

## 运行模拟器

这将是Havven系统的 代理模型。

在它可以运行之前，您将需要Python 3.6或更高版本并使用pip：

```pip install -r requirements.txt```

运行模拟器，调用

```python3 run.py```

运行结束后，如果正确，会出现

```
Caches saved to cache_data.pkl
Interface starting at http://127.0.0.1:3000
```
访问 http://127.0.0.1:3000/ 就能在界面上看到模拟过程

如果这是您第一次运行模拟，将生成`settings.ini`文件，这将使您可以控制模拟的运行方式。
第一个设置项`cached = True`确定在生成服务器之前是否预先生成数据，反之是否实时生成数据。
更多有关设置和缓存的信息，请参阅相关章节。

打开实验 notebook：

```jupyter notebook experiments.ipynb```

运行测试程序

```python -m pytest --pyargs -v```

Note: Running pytest through python3 is more consistent (global pytest install, other python versions).
The -v flag is for verbose, to list every individual test passing.
注意：用python3运行pytest能确认环境一致（其他python版本，pytest必须在全局安装）
-v 标志用于详细，列出每个单独的测试传递。

## 设置

设置在`settings.ini`中，文件将在第一次运行时使用`python run.py`命令生成，个别设置描述可以在`settingsloader.py`中找到。

## 缓存

更改缓存设置项会更改在本地网页上显示之前生成数据的方式。 如果缓存为真，则数据将预先生成，并以仅受连接速度限制的速率发送到客户端(`fps_default`设置项能控制此操作)。
否则，数据将实时呈现，由服务器生成，客户端可以请求下一步。

两者之间的另一个区别是更改模型设置。 如果缓存为真，则设置由`cache_handler.py`中的数据集设置确定。 如果缓存为false，则可以在客户端更改设置，然后由服务器使用新设置生成设置。

## 概述

该模拟有三个主要组成部分：

* Havven文本身的货币环境;
* 在nomins，havvens和fiat之间进行虚拟交换;
* 代理商本身， 可能的未来玩家：
    - [x] random players，随机玩家
    - [x] arbitrageurs，套利者
    - [x] havven bankers，havven 银行家 
    - [x] central bankers, 中央银行
    - [x] merchants / consumers, 商家/消费者
    - [x] market makers, 做市商
    - [x] buy-and-hold speculators, 买入并保持持有的投资者
    - [ ] day-trading speculators, 日内交易的投机者
    - [ ] cryptocurrency refugees, 加密货币的受害者
    - [ ] attackers, 攻击者

## 记住指南

它运行在[Mesa](https://github.com/projectmesa/mesa)上，包括以下文件和文件夹

* `run.py` - the main entry point for the program
* `reset.py` - script to clear and reset settings to default, and regenerate cache
* `server.py` - the simulation and visualisation server are instantiated here
* `model.py` - the actual ABM of Havven itself
* `core/orderbook.py` - an order book class for constructing markets between the three main currencies
* `core/stats.py` - statistical functions for examining interesting economic properties of the Havven model
* `core/settingsloader.py` - loads and generates settings files
* `core/cache_handler.py` - cached datasets are generated and loaded by this module
* `managers/` - helper classes for managing the Havven model's various parts
* `agents/` - economic actors who will interact with the model and the order book
* `test/` - the test suite
* `visualization/` - facilities for producing a live visualization web page
* `experiments.ipynb` - an environment for exploring system dynamics and scenarios in a more-efficient offline fashion.

> 翻译

* `run.py` - 程序的主要入口点
* `reset.py` - 用于清除和重置默认设置的脚本，并重新生成缓存
* `server.py` - 模拟和可视化服务器在这里实例化
* `model.py` - Havben本身的实际ABM
* `core/orderbook.py` - 用于在三种主要货币之间构建市场的订单簿类
* `core/stats.py` - 用于检查Havven模型的有趣经济属性的统计方法
* `core/settingsloader.py` - 加载并生成设置文件
* `core/cache_handler.py` - 此模块生成并加载缓存的数据集
* `managers /` - 用来管理Havven模型的各个部分的帮助类
* `agents/` - 将与模型和订单簿互动的经济参与者
* `test/` - 测试套件
* `visualization/` - 用于生成实时可视化网页的工具
* `experiments.ipynb` - 以更有效的离线方式探索系统动态和场景的环境。
