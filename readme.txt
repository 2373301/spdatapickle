tangfu д��
hi,��һ�£������ṩ�Ŀ���pb����ô������encode֮����ַ������Ƿ��ܹ�ʹ��protobuf��ParseFromString�����л�������


�� google �ṩ�Ŀ���ȫ���ݣ��������Եġ�


3 ¥ iunknown 2009-11-06  
���� 0.5 �汾������
1.protobuf ��һЩ bugfix
2.��ֲ�� win32 ƽ̨

http://spdatapickle.googlecode.com/files/spdatapickle-0.5.src.tar.gz
2 ¥ iunknown 2009-08-02  
���� 0.3 �汾���������� 
1.�����˶� ProtoBuf wire format ��֧�� 

[url]http://spdatapickle.googlecode.com/files/spdatapickle-0.3.src.tar.gz [/url]
1 ¥ iunknown 2009-08-02  
���� 0.2 �汾���������� 
1.�����˶� json ��֧�� 
2.xml pickle �� json pickle ��һ��ͳһ�Ľӿڣ�����ʹ�� 
3.�� metainfo ��֧��ָ��ĳ���ֶ��ǿ�ѡ�ģ��ڽ����ʱ�������Ӧ���ֶβ����ڣ�ֱ������ 

http://spdatapickle.googlecode.com/files/spdatapickle-0.2.src.tar.gz 

Java����  �ղش���
<metainfo prefix="XYZ" filename="addrbook">  
    <struct name="Email">  
        <field name="Type"    type="char" arraysize="10" />  
        <field name="Address" type="*char" />  
        <field name="Nickname" type="*char" required="0" />  
    </struct>  
</metainfo>  


Java����  �ղش���
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


���л��Ľ�� 
Java����  �ղش���
{  
        "Email" : {  
                "Type" : "work",  
                "Address" : "foo <foo@bar.com>"  
        }  
}  