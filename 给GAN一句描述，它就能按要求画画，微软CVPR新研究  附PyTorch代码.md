## 给GAN一句描述，它就能按要求画画，微软CVPR新研究 | 附PyTorch代码

关注前沿科技 [量子位](javascript:void(0);) *昨天*

##### 晓查 发自 凹非寺  量子位 报道 | 公众号 QbitAI

让AI认得图像，根据自己的理解给出一段叙述，已经不是什么新鲜事了。从图像到文字容易，把这个过程反过来却很难。

让AI画图有了成熟的解决方案，GAN就是是一个好办法，但是它通畅并不能按要求随心所欲造出图像。

而微软和京东AI研究院合作提出的**ObjGAN**就能做到这一点。ObjGAN可以理解一段说明文字，生成草图布局，并根据确切描述完善图像细节。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBavxBn5RfRYVsmibC6dogCQNqJQ8deHJR6RrsyibzTmlb1xUbyKBFkiccDNHicguaLZ95SuOdI8ezGag/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

他们的文章《Object-driven Text-to-Image Synthesis via Adversarial Training》已经被正在加州长滩举办的学术会议CVPR 2019收录。

## 应付多种场景

研究人员在文章中说，ObjGAN的生成器能够利用细节单词和对象级信息来逐步细化合成图像。这使得ObjGAN在生成图像细节时比之前的研究要强得多。

ObjGAN能生成多种场景下的小狗：一只棕色小狗躺在床上，或者是一只黑色小狗叼飞盘。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBavxBn5RfRYVsmibC6dogCQXia1IhUO23xiaoYn5JvMNX9kMq7h5UUhLJwT0YGM34UNxjELVXyV73Qw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

###### **△**左边是真实场景，中间两张由P-AttnGAN生成，右边两张由ObjGAN生成

如果说简单场景还看不出ObjGAN的厉害之处，那么下面两幅场景可以说是远远把对手甩在身后了。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBavxBn5RfRYVsmibC6dogCQOHJpDuWulc9aCbsHGFshialtACrXVdTU9FdZWj56ViaDeVhebIt8I2Kw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上一张是酒店房间，下一张是多种蔬菜水果，这两种场景下的对象非常多，P-AttnGAN已经翻车，除了画面混乱外，它还发生了理解错误的问题，把蓝色属性错误地放在床这个物体上。

为了证明Obj-GAN的泛化能力，研究人员不仅让它生成真实生活中的场景，甚至连不合常理的结果也可以“强行”生成。

比如让汽车火车停在水面上，让喵咪去叼飞盘或者下海游泳。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBavxBn5RfRYVsmibC6dogCQamsgKibD5LvSkHbVkYHJrvMKAYHAbEu6UIwoZZvkbVD57trjNzKt5DA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在客观指标上，Obj-GAN在大规模COCO基准测试的各种指标上优于先前的水平，Inception分数提高到了27，大大高于P-AttnGAN只有20左右的得分，FID也降低到了25.85。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBavxBn5RfRYVsmibC6dogCQWXKhDZ2PiaS8t7sZiaibTqGNmTu4QIwuaWhVw2ShWhLB8hlLFHicrzH7GA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## ObjGAN原理 

由文字描述生成图像的难点在于，如何让AI理解场景中多个对象之间的关系。ObjGAN通过关注文本描述中最相关的单词和预先生成的语义布局来合成对象。

以前的方法使用仅为单个对象提供粗粒度信号的图像-描述对，即使是性能最佳的模型也难以生成语义上有意义包含多个对象的图片。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBavxBn5RfRYVsmibC6dogCQjDw7Sybd860KNrt5AtTvYN2xDt0GBEL3DmicvGkPHMKN2rib5Vkw5AjA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

为了克服这些问题，研究人员提出了一种新的对象驱动的注意图像生成器，将图像生成分为构图和精细化图像两步。

此外，他们还提出了一种新的基于**Fast R-CNN**的逐对象鉴别器，提供关于合成对象是否与文本描述和预先生成布局匹配的识别信号。

最后，微软在这方面的研究不止ObjGAN一篇论文，他们还与腾讯AI研究院**StoryGAN**，也是从文本描述生成图像，同样被今年的CVPR收录。

## 传送门

论文地址：
https://arxiv.org/abs/1902.10740

PyTorch实现已开源：
https://github.com/jamesli1618/Obj-GAN

— **完** —

**AI社群 | 与优秀的人交流**

![img](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtBavxBn5RfRYVsmibC6dogCQvv70E942hsKiaqXajAINPb2sGlxLXxqX8tpUWvdg2Y7vxOpL2ryB3gw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**精选直播 | 大牛的观点碰撞**

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)



**量子位** QbitAI · 头条号签约作者





վ'ᴗ' ի 追踪AI技术和产品新动态



喜欢就点「好看」吧 !![img](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==) 















微信扫一扫
关注该公众号