#RTCSDK(Android)
2017-04-27
##1. RTCSDK简介
RTCSDK提供一对一和多对多的音视频会话与数据发送接收功能。如图1所示，图1(a)中展示的是A与B两点之间的音视频会话，图1(b)中展示的是A、B和C三点的音视频会话。

图1.RTCSDK的音视频会话功能
![](./RTCSDK/RTCSDK-conversation.png)
##2.RTCSDK音视频会话的建立
2.1 两点
A与B两点之间音视频会话的建立如图2所示。其中A是主叫，B是被叫。

图2 两点音视频会话的建立
![](./RTCSDK/RTCSDK-establish.png)

步骤：
1.主叫A调用RTCSDK接口CreatePeer，传入参数RTCParam，其中参数PeerID为被叫B的ID，参数sdp为NULL。（详见3.2RTCSDK参数）</br>
2.RTCSDK回调接口onRTCSDKMessage，其中PeerID为被叫B的ID，消	息类型type为MSG_CALLBACK_SDP_OFFER，消息msg为生成的sdp。</br>
3.4. 将sdp传递至被叫。</br>
5.被叫调用RTCSDK接口CreatePeer，传入参数RTCParam，其中参数PeerID为主叫A的ID，参数sdp为A生成的sdp。</br>
6.RTCSDK回调接口onRTCSDKMessage，其中PeerID为被叫A的ID，消息类型typ为MSG_CALLBACK_SDP_ANSWER，消息msg为生成的sdp。</br>
7.8. 将sdp传递至主叫。</br>
9 主叫调用RTCSDK接口  setRemoteDescription，其中参数PeerID为被叫B的ID，参数sdp为B生成的sdp。</br>
10	音视频连通，主叫和被叫的RTCSDK会通过接口onRTCSDKMessage回调MSG_ICE_CONNECTION。

###2.2 多点
多点音视频会话的建立与两点类似。以三点的音视频会话为例，如图1(b)所示，C在A与B已经建立完成音视频会话的基础上，再分别与A和B进行两点间的音视频会话的建立。
##3.RTCSDK接口
###3.1 创建与销毁RTCSDK
####3.1.1 创建
void createPeer(RTCParam param)
####3.1.2 销毁
void destroyPeer(String peerID)
###3.2 RTCSDK参数
	public class RTCParam {
	    private String peerId;   //多点，区分peerConnection
	    private String sdp = "";         //sdp
	    private Activity activity;//显示音视频的界面
	    private SurfaceViewRenderer localRender;
	    private SurfaceViewRenderer remoteRender;
	    private UserCallBack userListener; //回调监听
	    private String iceServer;//ip和端口合成一个
	    private String iceRelayServer;//中转 预留
	    private String iceRelayPort;  //中转 预留
	    private String iceUser; //ice用户登录名
	    private String icePwd;//ice用户登录密码
	    private int videoMaxBitrate; //最大码率
	    private int videoStartBitrate;//开始码率
	    private boolean isOpenVideo;//是否为视频
	};
####3.2.1 sdp
	主叫端在进行CreatePeer时，为""。被叫端在进行CreatePeer时，为主叫端生成的sdp。
###3.3 RTCSDK接口
	Class RTCSDK{
	 void createPeer(RTCParam param)；
	 void setRemoteDescription(String peerID, String sdp)
	 void destroyPeer(String peerID)；
	 void enableMicPhone(boolean isAudioEnableMicPhone)
	 void enableSpeaker(boolean isAudioEnableSpeaker)
	 void switchCamera()
	 void enableVideoSource(boolean enableVideoSource)
	 void turnVideoOff()
	}
####3.3.1 createPeer与setRemoteDescription
详见2.1节。
####3.3.2 destroyPeer
参数为空，释放所有资源。
传入peerID，释放与该peerID相关的资源。当只有一个peerID时，释放所有资源。
####3.3.3 enableSpeaker
打开/关闭外放
####3.3.4 turnVideoOff
在多人音视频中，将视频会话转换为音频会话，此过程不可逆。
####3.3.5 enableVideoSource
打开关闭本地视频的显示与发送，此过程可逆。
####3.3.6 enableMicPhone
打开/关闭话筒
###3.4 回调接口
	public interface UserCallBack {
	    public static final int MSG_CALLBACK_SDP_ANSWER = 101;
	   //呼叫或者接听后返回的字符  被叫
	    public static final int MSG_CALLBACK_SDP_OFFER = 102; 
	   //呼叫或者接听后返回的字符 主叫
	    public static final int MSG_ICE_CONNECTION = 103; 
	   //数据联通
	    public static final int MSG_ICE_DISCONNECTION = 104;
	   //数据断开
	    public static final int MSG_ICE_FAILES = 105; 
	    //数据链接失败（资源释放最好在该状态中）
	    public static final int MSG_PEERCONNECTION_ERROR = 106;
	   //呼叫数据出错
	    /**
	     * avsdk回调接口
	     *
	     * @param peerId peerID
	     * @param type   消息类型
	     * @param msg    返回的消息
	     */
	    void onRTCSDKMessage(String peerId, int type, String msg);
	}
####3.4.1 peerId
对方的id
####3.4.2 type
回调类型，详见常量定义节
####3.4.3 msg
回调数据，当type为MSG_CALLBACK_SDP_OFFER时，msg为主叫生成的sdp；当type为MSG_CALLBACK_SDP_ANSWER时，msg为被叫生成的sdp；
