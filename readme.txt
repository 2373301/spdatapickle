tangfu 写道
hi,问一下，博主提供的库与pb兼容么，比如encode之后的字符串，是否能够使用protobuf的ParseFromString反序列化回来？


和 google 提供的库完全兼容，做过测试的。


3 楼 iunknown 2009-11-06  
发布 0.5 版本，包括
1.protobuf 的一些 bugfix
2.移植到 win32 平台

http://spdatapickle.googlecode.com/files/spdatapickle-0.5.src.tar.gz
2 楼 iunknown 2009-08-02  
发布 0.3 版本，新增特性 
1.增加了对 ProtoBuf wire format 的支持 

[url]http://spdatapickle.googlecode.com/files/spdatapickle-0.3.src.tar.gz [/url]
1 楼 iunknown 2009-08-02  
发布 0.2 版本，新增特性 
1.增加了对 json 的支持 
2.xml pickle 和 json pickle 用一个统一的接口，方便使用 
3.在 metainfo 中支持指定某个字段是可选的，在解包的时候，如果对应的字段不存在，直接跳过 

http://spdatapickle.googlecode.com/files/spdatapickle-0.2.src.tar.gz 

Java代码  收藏代码
<metainfo prefix="XYZ" filename="addrbook">  
    <struct name="Email">  
        <field name="Type"    type="char" arraysize="10" />  
        <field name="Address" type="*char" />  
        <field name="Nickname" type="*char" required="0" />  
    </struct>  
</metainfo>  


Java代码  收藏代码
void testEmail( SP_DataPickle * pickle )  
{  
    XYZEmail_t email;  
    memset( &email, 0, sizeof( email ) );  
  
    strncpy( email.mType, "work", sizeof( email.mType ) - 1 );  
    email.mAddress = strdup( "foo <foo@bar.com>" );  
  
    SP_XmlStringBuffer buffer;  
  
    pickle->pickle( &email, sizeof( email ), eTypeXYZEmail, &buffer );  
  
    printf( "%s\n\n", buffer.getBuffer() );  
  
    SP_DPAlloc alloc( gXYZAddrbookMetaInfo );  
    alloc.free( &email, sizeof( email ), eTypeXYZEmail );  
}  


序列化的结果 
Java代码  收藏代码
{  
        "Email" : {  
                "Type" : "work",  
                "Address" : "foo <foo@bar.com>"  
        }  
}  