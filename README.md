# face-recognition
从收集照片开始，建立一个简单的人脸识别模型
    最近在复习吴恩达老师的deeplearning.ai课程，所谓温故而知新，看到人脸识别时，很多以前没有彻底明白的知识现在感觉豁然开朗，思路清晰了很多，
于是很想自己从头到尾，从收集自己的照片开始来做一个人脸识别。新手上路，欢迎交流！
    与人脸识别相近的还有人脸验证，即验证输入图片与声称的是否是同一个人，例如现在大多的火车站，机场进站时都有人脸验证，旅客进入操作区，系统扫
描身份证车票等信息，验证是否为声称的人；支付宝等手机APP上也有人脸验证，每次应用时与之前帐户录入的照片做比对判断是否为用户，综上所述，人脸验证
是1：1问题。比人脸验证更复杂的是，人脸识别是1：k问题 ，例如有个包含k个人的图片库，识别新输入的图片是k个人中的哪一个，或者哪个都不是，现在有的
公司就有应用人脸识别做门禁，预先把员工人脸图片输入系统，当有人员进入时，就去系统内寻找是哪一个人。
   我这里要重点讲的就是人脸识别。深度学习效果好，很大程度上是基于大量训练样本的，而实际的应用中通常只有少量照片，要如何解决这个问题呢？假如在
公司的员工图片库里，可能只有每个员工的几张照片，如果按照其他问题深度学习的常用方法，将所有图片输入网络，最后利用softmax分类输出标签，但是训练
集太小效果会很差，并且当有新员工加入时，还需要重新训练网络。这时，我们就可以学习一个 ’similarity function’ 来解决问题。
d(img1,img2)  =  degree of defference between images,如果输入两张长相差别很大的人，那么d(img1,img2)就很大，如果输入两张同一个人的照片或者
长相相似的人的照片，d(img1,img2)就很小。要学习这个函数的一个方法就是应用Siamese网络。
    由于收集照片比较耗时，为了能有足够的标签为1（同一个人）的照片，我收集了七个人（包括我一家三口，还有网上找的吴恩达老师，习大大，刘亦菲，
胡歌的照片），每个人大约30张照片，然后positive_pairs(同一个人)随机生成5000对，negative_pairs(不同的人)随机生成5000对，输入一个Siamese卷积
网络，生成128维的编码对，通过一个逻辑回归单元进行二分类，利用反向传播优化网络参数

   图片我只上传了吴恩达老师，习大大，刘亦菲，胡歌的照片，我一家三口的照片就不上传了。。。
