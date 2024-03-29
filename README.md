# kubeadm-certs

##在/etc/kubernetes/pki目录下证书的分类：
密钥对：sa.key sa.pub
根证书：ca.crt etcd的ca.crt
私钥 ：ca.key

##service Account密钥对 sa.key sa.pub
提供给 kube-controller-manager 使用. kube-controller-manager 通过 sa.key 对 token 进行签名, master 节点通过公钥 sa.pub 进行签名的验证
如 kube-proxy 是以 pod 形式运行的, 在 pod 中, 直接使用 service account 与 kube-apiserver 进行认证, 此时就不需要再单独为 kube-proxy 创建证书了, 会直接使用token校验

##根证书
pki/ca.crt
pki/ca.key

##apiserver 证书
pki/apiserver.crt
pki/apiserver.key

##kubelet证书
pki/apiserver-kubelet-client.crt
pki/apiserver-kubelet-client.key

##Aggregation 证书
代理根证书：
pki/front-proxy-ca.crt
pki/front-proxy-ca.key
由代理根证书签发的客户端证书：
pki/front-proxy-client.crt
pki/front-proxy-client.key
比如使用kubectl proxy代理访问时，kube-apiserver使用这个证书来验证客户端证书是否是自己签发的证书。

##etcd 根证书
pki/etcd/ca.crt
pki/etcd/ca.key
etcd节点间相互通信 peer证书
pki/etcd/peer.crt
pki/etcd/peer.key

##pod中Liveness探针客户端证书
pki/etcd/healthcheck-client.crt
pki/etcd/healthcheck-client.key

##apiserver访问etcd的证书
pki/apiserver-etcd-client.crt
pki/apiserver-etcd-client.key
