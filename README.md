# database-migration-onprem-to-aws
This project provides a step-by-step guide on how to migrate a WordPress website and MariaDB database from on-premises to AWS, using peering connections and AWS services such as EC2, RDS, and DMS. The guide covers setting up the simulated environment, creating VPC and peering connection, launching instances, setting up DMS replication, and testing.

![dms](https://user-images.githubusercontent.com/116753469/227190460-ae837c2a-28b6-4c36-b11b-477cf6747536.png)


## Installation
To use this project, you need to have the following:
- A simulated AWS on-prem env with a WordPress website and MariaDB database.
- An AWS account with access to EC2, RDS, and DMS.


## The guide covers the following steps:
1. Assuming a simulated on-premises environment on AWS with a WordPress website and MariaDB database are already setup.
2. Create an AWS VPC and peering connection between the on-premises (simulated) environment and the AWS VPC.
3. Launch an EC2 instance in the AWS VPC and configure it as the new webserver for the WordPress website.
4. Launch an RDS instance in the AWS VPC and configure it as the new database server for the MariaDB database.
5. Set up DMS replication instance between the on-premises MariaDB database and the AWS RDS instance and start replicating.
6. Test the migrated WordPress website by modifying the wordpress file where the ip is pointed to on-prem to DNS of MariaDB database.
7. As a cleanup delete the instances, peering connection, DMS replication instance, RDS, EC2, etc.

<img width="1156" alt="Snipaste_2023-03-23_17-05-08" src="https://user-images.githubusercontent.com/116753469/227181289-57823415-18d4-4f00-8d8e-324ad7fa6797.png">
<img width="1156" alt="Snipaste_2023-03-23_17-06-28" src="https://user-images.githubusercontent.com/116753469/227181299-4e34fd22-5c16-4f84-8128-b19071db21a2.png">
<img width="472" alt="Snipaste_2023-03-23_17-07-51" src="https://user-images.githubusercontent.com/116753469/227181300-69cc6bf6-5a0e-4b37-bd34-4c5950b121fd.png">
<img width="1190" alt="Snipaste_2023-03-23_17-08-34" src="https://user-images.githubusercontent.com/116753469/227181307-df1bebf3-3391-4bc9-8a7d-753775a41007.png">
<img width="1156" alt="Snipaste_2023-03-23_17-08-59" src="https://user-images.githubusercontent.com/116753469/227181312-ca73feb3-4941-4e38-aa01-a6d0bcd47f04.png">
<img width="1177" alt="Snipaste_2023-03-23_17-16-40" src="https://user-images.githubusercontent.com/116753469/227181318-b37508d3-5891-4e15-9434-2e9593820ea7.png">
<img width="1415" alt="Snipaste_2023-03-23_17-17-56" src="https://user-images.githubusercontent.com/116753469/227181322-e84728d6-a8d8-4915-881e-8e27c18aaeb1.png">
<img width="1165" alt="Snipaste_2023-03-23_17-19-07" src="https://user-images.githubusercontent.com/116753469/227181325-25f3a721-3337-46be-992d-ae07212fd0ad.png">
<img width="1153" alt="Snipaste_2023-03-23_17-19-44" src="https://user-images.githubusercontent.com/116753469/227181332-14a98300-f45d-4d5b-9efd-fe16a13dac09.png">
<img width="1440" alt="Snipaste_2023-03-23_17-20-41" src="https://user-images.githubusercontent.com/116753469/227181336-01f02e9d-9b39-4a40-aabd-cd6b5261b129.png">
<img width="1190" alt="Snipaste_2023-03-23_17-21-12" src="https://user-images.githubusercontent.com/116753469/227181337-b2282e3c-739b-4916-9294-52b208c3eb2f.png">
<img width="1432" alt="Snipaste_2023-03-23_17-21-39" src="https://user-images.githubusercontent.com/116753469/227181343-7dd7eed4-24aa-46d3-9704-cf5a1a79caae.png">
<img width="1157" alt="Snipaste_2023-03-23_17-23-41" src="https://user-images.githubusercontent.com/116753469/227181345-aa3e0112-01e5-4b66-a877-a86dea2f3f4a.png">
<img width="1146" alt="Snipaste_2023-03-23_17-26-10" src="https://user-images.githubusercontent.com/116753469/227181346-39be9004-ce9c-447e-b1a3-c09c093ea43c.png">
<img width="1410" alt="Snipaste_2023-03-23_17-35-09" src="https://user-images.githubusercontent.com/116753469/227181349-9f24e11e-1215-414a-9021-984958b052d9.png">
<img width="448" alt="Snipaste_2023-03-23_17-38-33" src="https://user-images.githubusercontent.com/116753469/227181350-17fa72a1-7388-49ad-a6ac-7046d899cbb5.png">
<img width="1156" alt="Snipaste_2023-03-23_17-38-59" src="https://user-images.githubusercontent.com/116753469/227181352-391fc823-d393-4f62-bde7-5d733f67be97.png">
<img width="1008" alt="Snipaste_2023-03-23_17-40-16" src="https://user-images.githubusercontent.com/116753469/227181358-2bdca51d-4bc7-445e-830d-57d69ae7f17a.png">
<img width="851" alt="Snipaste_2023-03-23_17-42-15" src="https://user-images.githubusercontent.com/116753469/227181360-fecc131d-1be6-4de3-9afc-5be69d53615a.png">
<img width="726" alt="Snipaste_2023-03-23_17-43-14" src="https://user-images.githubusercontent.com/116753469/227181363-96a728c0-16d2-43bc-b2a0-c6128e6fd149.png">
<img width="701" alt="Snipaste_2023-03-23_17-44-38" src="https://user-images.githubusercontent.com/116753469/227181364-c8852245-a24d-43fa-b160-88c86066591c.png">
<img width="643" alt="Snipaste_2023-03-23_17-46-20" src="https://user-images.githubusercontent.com/116753469/227181367-a726d4c0-a3a2-430d-aac6-9059cf62a761.png">
<img width="1231" alt="Snipaste_2023-03-23_17-47-26" src="https://user-images.githubusercontent.com/116753469/227181373-f300acf3-0f85-4c56-82fa-93ae1fd5c033.png">
<img width="685" alt="Snipaste_2023-03-23_17-47-43" src="https://user-images.githubusercontent.com/116753469/227181376-b44e20dc-247e-4524-a978-9440f9a3189c.png">
<img width="668" alt="Snipaste_2023-03-23_17-48-42" src="https://user-images.githubusercontent.com/116753469/227181377-284bbec8-2d24-4218-a9c3-8c915d865de4.png">
<img width="1068" alt="Snipaste_2023-03-23_17-49-56" src="https://user-images.githubusercontent.com/116753469/227181380-292a286f-b2bd-4f81-910e-9c86be36f688.png">
<img width="738" alt="Snipaste_2023-03-23_17-50-23" src="https://user-images.githubusercontent.com/116753469/227181383-17661b4a-db52-4115-8547-58dac37950b7.png">
<img width="1243" alt="Snipaste_2023-03-23_17-51-54" src="https://user-images.githubusercontent.com/116753469/227181385-d946c6be-95ef-45f9-8921-193ebf4778c2.png">
<img width="664" alt="Snipaste_2023-03-23_17-54-05" src="https://user-images.githubusercontent.com/116753469/227181388-36147e78-350f-4cbf-806a-93075012a1f8.png">
<img width="644" alt="Snipaste_2023-03-23_17-54-41" src="https://user-images.githubusercontent.com/116753469/227181392-beb4a5bf-50dd-4487-a974-ddd01ce83aef.png">
<img width="1239" alt="Snipaste_2023-03-23_17-55-57" src="https://user-images.githubusercontent.com/116753469/227181395-716964e1-2d68-4b68-8593-23c3725a7a2e.png">
<img width="621" alt="Snipaste_2023-03-23_17-56-16" src="https://user-images.githubusercontent.com/116753469/227181398-7144ee84-f64f-4cfc-a6e4-98a2334dd24c.png">
<img width="1194" alt="Snipaste_2023-03-23_17-58-03" src="https://user-images.githubusercontent.com/116753469/227181401-a70ba4bb-beca-46fd-b67c-37236b15519b.png">
<img width="1182" alt="Snipaste_2023-03-23_17-58-17" src="https://user-images.githubusercontent.com/116753469/227181404-8d92a1d2-146e-431e-a7da-3aa463851453.png">
<img width="653" alt="Snipaste_2023-03-23_17-58-32" src="https://user-images.githubusercontent.com/116753469/227181406-86b6b37e-a850-4c72-b22d-f4d01b95e175.png">
<img width="1240" alt="Snipaste_2023-03-23_17-59-05" src="https://user-images.githubusercontent.com/116753469/227181409-aa41d1c9-aa82-4fd7-b4d6-420af1162d93.png">
<img width="1238" alt="Snipaste_2023-03-23_18-01-21" src="https://user-images.githubusercontent.com/116753469/227181412-82184347-ab8d-48c0-b140-e3f6cd9d450d.png">
<img width="1236" alt="Snipaste_2023-03-23_18-01-59" src="https://user-images.githubusercontent.com/116753469/227181416-b8a8df02-9478-4b4d-b522-1df79d73f514.png">
<img width="745" alt="Snipaste_2023-03-23_18-02-57" src="https://user-images.githubusercontent.com/116753469/227181419-7cf76706-84dd-4576-bab0-442f9f5c4d5e.png">
<img width="1227" alt="Snipaste_2023-03-23_18-03-52" src="https://user-images.githubusercontent.com/116753469/227181422-f6a82897-e583-430c-9883-667917e0726e.png">
<img width="1433" alt="Snipaste_2023-03-23_18-04-42" src="https://user-images.githubusercontent.com/116753469/227181424-485190ed-9697-46de-bca9-55ece33e3a17.png">
<img width="1414" alt="Snipaste_2023-03-23_18-06-48" src="https://user-images.githubusercontent.com/116753469/227181430-9dae4bce-aa25-449c-82f1-fe0e22c2ed71.png">
<img width="896" alt="Snipaste_2023-03-23_18-08-08" src="https://user-images.githubusercontent.com/116753469/227181433-1e185f4e-a19e-4cf9-81d6-c4a13cdd651a.png">
<img width="668" alt="Snipaste_2023-03-23_18-10-56" src="https://user-images.githubusercontent.com/116753469/227181439-f7784479-295f-446c-a8cb-b5fe1bbc4680.png">
<img width="531" alt="Snipaste_2023-03-23_18-16-02" src="https://user-images.githubusercontent.com/116753469/227181443-5a911a6c-9ea5-42a6-8829-2bfe34a8635b.png">
<img width="1238" alt="Snipaste_2023-03-23_18-17-12" src="https://user-images.githubusercontent.com/116753469/227181445-283a12f7-fa2c-458a-b521-03f63d5ff064.png">
<img width="1439" alt="Snipaste_2023-03-23_18-19-50" src="https://user-images.githubusercontent.com/116753469/227181449-678c0c3c-4b1e-4f5c-ae0e-9e661f091660.png">
<img width="1440" alt="Snipaste_2023-03-23_18-23-02" src="https://user-images.githubusercontent.com/116753469/227181452-4da21ca5-641c-4f8e-8c34-f8ad32e966cf.png">
<img width="647" alt="Snipaste_2023-03-23_18-24-06" src="https://user-images.githubusercontent.com/116753469/227181453-d0628993-05ab-4653-9f45-24b2ac956401.png">
<img width="1240" alt="Snipaste_2023-03-23_18-24-40" src="https://user-images.githubusercontent.com/116753469/227181456-fe82f27e-afd7-4dfd-8725-c789a995c766.png">
<img width="1194" alt="Snipaste_2023-03-23_18-28-38" src="https://user-images.githubusercontent.com/116753469/227181460-609557ec-b2ca-4d0f-9acd-1ce40dd22b9c.png">
<img width="747" alt="Snipaste_2023-03-23_18-31-20" src="https://user-images.githubusercontent.com/116753469/227181462-2fde629a-81dc-40db-876d-48c5c25725c4.png">
<img width="1436" alt="Snipaste_2023-03-23_18-32-03" src="https://user-images.githubusercontent.com/116753469/227181465-8b41c292-5cf4-49f1-97f9-5fa0c528c771.png">
<img width="802" alt="Snipaste_2023-03-23_18-33-27" src="https://user-images.githubusercontent.com/116753469/227181466-db0f0a54-11a3-4379-81a6-7146220b23d9.png">
<img width="1415" alt="Snipaste_2023-03-23_18-34-00" src="https://user-images.githubusercontent.com/116753469/227181471-4a9a2371-f484-48a8-9d2b-d3d202f0012e.png">
<img width="799" alt="Snipaste_2023-03-23_18-36-15" src="https://user-images.githubusercontent.com/116753469/227181477-704298ae-c6d6-4ed7-9ce2-22e2392aff40.png">
<img width="730" alt="Snipaste_2023-03-23_18-36-40" src="https://user-images.githubusercontent.com/116753469/227181479-8254b252-b55b-4f81-9e9c-09404d43e286.png">
<img width="1252" alt="Snipaste_2023-03-23_18-37-35" src="https://user-images.githubusercontent.com/116753469/227181481-53f5915f-0881-464b-8df2-76faf40b0e3c.png">
<img width="733" alt="Snipaste_2023-03-23_18-37-52" src="https://user-images.githubusercontent.com/116753469/227181486-e0d83cb6-f10d-4fe4-987e-0041067eadc6.png">
<img width="1430" alt="Snipaste_2023-03-23_18-38-31" src="https://user-images.githubusercontent.com/116753469/227181488-a533b33b-de2d-4476-b025-b8fc16e7ac4f.png">
<img width="512" alt="Snipaste_2023-03-23_18-42-38" src="https://user-images.githubusercontent.com/116753469/227181492-6e656fb3-652a-4e75-a3db-1ea27aa8d018.png">
<img width="852" alt="Snipaste_2023-03-23_18-46-38" src="https://user-images.githubusercontent.com/116753469/227181495-92a24db3-5a2c-4448-b750-a32b2ddac4a6.png">
<img width="932" alt="Snipaste_2023-03-23_18-47-13" src="https://user-images.githubusercontent.com/116753469/227181497-68a38c6b-bfce-48c0-8aa0-d1baa1f035c6.png">
<img width="1013" alt="Snipaste_2023-03-23_18-55-21" src="https://user-images.githubusercontent.com/116753469/227181502-365f6a42-6b5e-4113-8ff3-ee82b21eff80.png">
<img width="1440" alt="Snipaste_2023-03-23_18-55-50" src="https://user-images.githubusercontent.com/116753469/227181506-27ae3890-572c-4630-a27d-735f1591ba29.png">
<img width="801" alt="Snipaste_2023-03-23_19-00-37" src="https://user-images.githubusercontent.com/116753469/227181508-10d692cf-8bcb-4139-9d65-82e1abe50542.png">
<img width="804" alt="Snipaste_2023-03-23_19-01-04" src="https://user-images.githubusercontent.com/116753469/227181513-616f544f-d5df-4e4d-be1e-9c985c87e8fe.png">
<img width="1206" alt="Snipaste_2023-03-23_19-01-57" src="https://user-images.githubusercontent.com/116753469/227181518-67feadd4-f431-4bd2-a475-724790f392e3.png">
<img width="1243" alt="Snipaste_2023-03-23_19-02-44" src="https://user-images.githubusercontent.com/116753469/227181521-544fbe1d-baf4-457b-96a1-2784c45a5eba.png">
<img width="972" alt="Snipaste_2023-03-23_19-06-03" src="https://user-images.githubusercontent.com/116753469/227181523-1d78e255-779a-4094-adb2-5e94176bc21b.png">
<img width="1184" alt="Snipaste_2023-03-23_19-07-38" src="https://user-images.githubusercontent.com/116753469/227181525-6edd73e1-5abd-4f3d-a085-6f7c815832e7.png">
<img width="1253" alt="Snipaste_2023-03-23_19-09-54" src="https://user-images.githubusercontent.com/116753469/227181531-a0a9a9d7-9718-449b-afc5-7c10955a8aa9.png">
<img width="1237" alt="Snipaste_2023-03-23_19-12-56" src="https://user-images.githubusercontent.com/116753469/227181532-130d9888-31eb-4ae4-bc4b-d25892fc100a.png">
<img width="1239" alt="Snipaste_2023-03-23_19-13-09" src="https://user-images.githubusercontent.com/116753469/227181535-ca4c3368-e614-4149-b59e-de3b41b26058.png">
<img width="1091" alt="Snipaste_2023-03-23_19-16-18" src="https://user-images.githubusercontent.com/116753469/227181541-97a947ec-9990-40ad-8fcd-9569baf0659a.png">


## CleanUp:
At the end as a cleanup delete the instances, peering connection, DMS replication instance, RDS, EC2, etc.
