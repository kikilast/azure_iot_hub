# Azure iot hub Device Twin

## �˸m������

### ²��
�C���@�Ӹ˸m�s�u��iot hub �A�N�|���ͤ@�ӹ������˸m�������A�HJSON����Ʈ榡���x�s�˸m��������T�A�]�Ametadata, configuration, condition �C�˸m�������O�i�H���V���q��(D2C,C2D)�A�bAzure IoT hub ���t�m���O�ݩ�зǼh�~�i�H�ϥΪ��C�˸m�������i�H�b�����x�s�S�w�����~��ơB�q�˸m�����ε{�����o���ثe�˸m�����p�B�P�B�B�z�˸m�ݩM��ݪ��u�@�y�{���A(��s���)�B�d�߸˸m����T
### ��󤺮e
JSON��󤤦��|�ӳ���
-  Tags:��ݥi�HŪ���M�g�J��json�����A�˸m�ݬݤ���
-  Desired properties:���˸m�ݪ����ε{���i�H������ݪ��ݨD
-  Reported properties:����ݤF�Ѹ˸m�ݪ����p�٦��i�HŪ���d��
   *desired properties �M reported properties �ݤ��۷f�t�ϥΡA�ӦP�B�B�z�t�m�պA�Ϊ��p
-  Device identity properties:�����˸m��metadata

![alt tag](https://i.imgur.com/VKWL43U.png)

![alt tag](https://i.imgur.com/gpPIzpF.png)

���ҡB�һ��ݩʩM���i�ݩʥ����䴩�}�񦡨æ�s��
Etag�O�ΨӽT�O���Ҹ�ƪ��@�P�ʡA��version�h�|�̷Ӫ��������P���@�ӻ��W���A��s�ݥi�H�ϥΪ����j��F���s���@�P��(�קK�˸m�M���ݦP�ɦs����Ƴy����T���@�P)
$ �N��Ӹ�ƫǰ�Ū�ݩ�
���ҡB�һ��ݩʩM���i�ݩʤ��Ҧ� JSON ���󪺲`�פW���� 5�C
�Ҧ��r��Ȫ��̤j���׬� 4 KB

## D2C
���Ʊq�e�ݸ˸m���ݪ��ѨM��ת��ɭԡA�i�w��ǿ骺���A���ѤT�Ӥ覡
1. �˸m�춳�ݰT��
2. �˸m���������^���ݩ�
3. �W���ɮ�

![alt tag](https://i.imgur.com/XxTlSGb.png)

*��ڦ��ݭn�ǰe������T�άOĵ�ܪ��ɭԡA����ذ��k�i�H��D2C���覡�ǰe�άO���a�b���Ҥ��A���O��ĳ���n�ϥβĤG�ءA�ѩ�˸m�춳�ݰT�����\����˸m��������s����e�q�A�ҥH���ɧƱ��קK�w��C�h�˸m�춳�ݰT����s�˸m�������C

![alt tag](https://i.imgur.com/wkEghgS.png)

## C2D
Iot hub ����3�ӱq�˸m�ݨ춳�ݪ��\��
1. ������k:�ݭn�ߧY�T�{���G���q�T�A�q�`�Ω�˸m�����ʦ�����A�Ҧp�}�ҭ����C
2. ���������һ��ݩʡA�A�Ω�i���˸m�i�J�S�w�һݪ��A�����ɶ�����R�O�C �Ҧp�A�N�����ǰe���j�]�w�� 30 �����C
3. ���ݨ�˸m�T���A�A�Ω��˸m���ε{������V�q���C


![alt tag](https://i.imgur.com/QBTQtt9.png)

![alt tag](https://i.imgur.com/51qPOVM.png)

## �˸m�P�Ҳչ������B�@�~�M�T�����Ѫ� IoT ���Ϭd�߻y��

Source: https://docs.microsoft.com/zh-tw/azure/iot-hub/iot-hub-devguide-query-language

�C�ӡuIoT ���ϡv�d�߳��]�t SELECT �M FROM �l�y�A�H�ο�ܩʪ� WHERE �M GROUP BY �l�y�C �C�Ӭd�߳��|�b JSON ��󪺶��X�W����A�Ҧp�˸m�������C FROM �l�y�|���X�n�b��W���йB�⪺��󶰦X (devices �� devices.jobs)�C �M��A�|�M�� WHERE �l�y�����z��C �ϥηJ�`�ɡA���B�J�����G�|�̷� GROUP BY �l�y���ҫ��w���覡�i����աC �w��C�Ӹs�աA�|�̷� SELECT �l�y���ҫ��w���覡���ͤ@�Ӹ�ƦC�C

### FROM �l�y
FROM <from_specification> �l�y�u��ĥΨ�ӭȡJFROM devices (�ΨӬd�߸˸m������) �� FROM devices.jobs (�ΨӬd�ߨC�@�˸m���@�~�ԲӸ��)�C

### WHERE �l�y
WHERE <filter_condition> �l�y�O��ܩʪ��C ���|���w�@�Φh�ӱ���A�ӥB FROM ���X���� JSON ��󥲶������o�Ǳ���A�~��ǤJ�����G���@�����C ���� JSON ��󳣥����N���w����������� "true"�A�~��֤J���G�C
�B�⦡�M����@�`���|�������\������C

### SELECT �l�y
SELECT <select_list> �O���n�l�y�A�i���w�n�q�d���^�����ȡC ���|���w�ΨӲ��ͷs JSON ���� JSON �ȡC �w��w�z�� (�ε��ݭn�w����) �� FROM ���X�l�����C�Ӷ��ءA��v���q�|���ͤ@�ӷs�� JSON ����C ������|�H SELECT �l�y���ҫ��w���Ȩӫغc�C

### GROUP BY �l�y
GROUP BY <group_specification> �l�y�O�@�ӿ�ܩʨB�J�A�|�b WHERE �l�y�����w���z�蠟��BSELECT �����w����v���e����C ���|�ھ��ݩʭȨӤ��դ��C �o�Ǹs�եi�ΨӲ��� SELECT �l�y���ҫ��w���J�`�ȡC
