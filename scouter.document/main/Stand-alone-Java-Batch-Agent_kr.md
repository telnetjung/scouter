# Stand-alone Java Batch Agent

��ī���� APM�� WAS �Ӹ� �ƴ϶� ��ġ ����͸� ��ɵ� �����Ѵ�.
��ġ�� �Ϲ������� �뷮 ���� ó���ϴ� ��찡 ���� �Ϲ� APM���δ� ����͸��� �Ѱ谡 �־���. ��ī���ʹ� ��ġ Ư���� �����Ͽ� ��� �߽����� ������ �м������� �ڹ� �Լ� �������� �м��� �� �ִ�.

��ī���� ��ġ ������Ʈ�� �Ʒ��� ���� ����� �����Ѵ�.
- ����ð� ����(CPU ��뷮)
- SQL �������ϸ�(SQL��, SQL ����ð�, SQL ó���Ǽ�, SQL ����Ƚ��)
- �ֱ����� ���μ��� ���� ����  

## �ν��� ����
��ī���� ������ Ŭ���̾�Ʈ�� ��ġ�Ǿ� �ִٸ� �Ʒ� �δܰ踦 ��ġ�� �ڹ� ��ġ ����͸��� �����ϴ�.
####1. �ڹ� ��ġ ���μ����� �ɼ� �߰�(����: �ڹٿɼ�)
####2. ��ī���� ��ġ ���� ����(����: �ڹ� ������Ʈ�� ������)

## �ڹ� �ɼ�
��ī���� ��ġ ������Ʈ�� �⺻ ��ġ ����� WAS ��� �ڹ� ������Ʈ�� �����ϴ�.
�ڹ� ��ġ ���� ����(�� ��ũ��Ʈ ����)�� -javaagent�� -Dscouter.config ������ �߰��ϸ� ����͸��� �����ϴ�.

```
JAVA_OPTS=" ${JAVA_OPTS} -javaagent:${SCOUTER_AGENT_DIR}/scouter.agent.batch.jar"
JAVA_OPTS=" ${JAVA_OPTS} -Dscouter.config=${SCOUTER_AGENT_DIR}/scouter.batch.conf"
```

## ȯ�漳��

### ȯ�漳�� ����
`${SCOUTER_AGENT_DIR}/scouter.batch.conf` ���� ȯ�漳�� ������ �����ϰ�, ������ ���������ν� ���� �ɼ��� ������ �� �ִ�.
> �ɼ��� ������ �⺻ ���� ����ȴ�.

### ��
*${appropriate_directory}/scouter.batch.conf*
```
# Stand-Alone mode
scouter_standalone=false

# Batch ID (batch_id_type: class,args,props) (batch_id: args->index number, props->key string)
batch_id_type=args
batch_id=0

# Scouter Server IP Address (Default : 127.0.0.1)
net_collector_ip=127.0.0.1

# Scouter Server Port (Default : 6100)
net_collector_udp_port=6100
net_collector_tcp_port=6100

# Scouter Name(Default : batch)
obj_name=exbatch
```
***

###  ȯ�漳�� ��
�׸�     |    �⺻ ��    | ����
------------ | -------------- | --------------
scouter_enabled | true | ��ī���� �ڹ� ��ġ ���̾�Ʈ�� ����͸��� ���� ���θ� ������(true - ����͸� ����)
scouter_standalone | false | ��ī���� ������ ����͸� ����� ������ �� ���θ� ������(true - ��ī���� ������ ����͸� ��� ����). false�� �����ϸ� log_dir�� ����͸� ����� ��ġ ���� ����͸�(sbr����)�� ���� �α�(log����)�� �����. true�� ���� ����͸��� ���� ������ �ʰ� ���� �α� ������ ���� ���� �� ���� �Ѵ�.
batch_id_type | class | ��ġ JOB ID�� �����ϴ� ��Ģ ����(class - ��ġ ���μ��� ���� �ڹ� Ŭ������ JOB ID�� ����, args - ���� Ŭ���� �ڿ� �߰� ������ �Ķ������ �Ѱ��� JOB ID�� ����, props - JVM ���� �Ķ������ �� ���� JOB ID�� ����) 
batch_id |       | batch_id_type ������ ���� JOB ID ������ ���� ���� ������. batch_id_type�� ���� �ǹ̰� �ٸ�(args - ���� ���ɿ� �߰��� �Ķ���Ϳ��� JOB ID�� ���� ��ġ(0���� ����), props - JVM ���� �Ķ������ �̸�(��: -DjobID=TEST001 �̸� ���� ���� jobID)) 
sql_enabled | true | SQL ���� ��� ���� ���� ����(true - SQL ��� ����)
sql_max_count | 100 | SQL ���� ��� ���� �� ����͸��� �ִ� SQL ��(����� SQL���� �⺻ ���� 100������ ������ ������ SQL������ ��ü�� �ϳ��� SQL�� ���� ������ SQL���� "Others"�� ��ϵ�)
hook_jdbc_pstmt_classes |  | SQL ���� ��� ������ ���� �⺻ ������ JDBC PreparedStatement Ŭ���� �̿� �ٸ� PreparedStatement Ŭ������ �߰��� �� �ش� Ŭ���� ���� �߰���(���� ��ȣ�� ��ǥ(,))
hook_jdbc_stmt_classes |  | SQL ���� ��� ������ ���� �⺻ ������ JDBC Statement Ŭ���� �̿� �ٸ� Statement Ŭ������ �߰��� �� �ش� Ŭ���� ���� �߰���(���� ��ȣ�� ��ǥ(,))
hook_jdbc_rs_classes |  | SQL ���� ��� ������ ���� �⺻ ������ JDBC ResultSet Ŭ���� �̿� �ٸ� ResultSet Ŭ������ �߰��� �� �ش� Ŭ���� ���� �߰���(���� ��ȣ�� ��ǥ(,))
sfa_dump_enabled | true | �ڹ� ��ġ ���� �ÿ� �ֱ������� ������ �����Ͽ� �Լ� �������� ������ �м��� �� �ֵ��� �ϴ� ���(true - ���� ����). ���� �м� �ÿ��� Stack Frequency Analyzer�� �����
sfa_dump_interval_ms | 10000 | �ڹ� ��ġ ���� ���� �ֱ� ����(�и���)
sfa_dump_filter |  | ���� �� Ư�� ���ڿ��� �� �ִ� ��쿡�� �����Ͽ� ������ ������ ��쿡 ���͸� ������(���Ͱ� �����ڴ� ��ǥ(,) ���). �����Ǵ� ������ ���� �ٿ� ��ü �α� ���� ũ�⸦ ���̰��� �� �� �����
sfa_dump_dir | ������Ʈ ���丮 �� dump | ���� �α� ������ ���� ���丮�� ������(�⺻: �ڹ� ��ġ ������Ʈ�� ��ġ�� Ȩ ���丮 �Ʒ� dump ���丮�� ����). ��ī���� ������ ������ �̷������ ���� �α� ������ ������
sfa_dump_header_exists | true | ���� �����ÿ� ���� �ð��� JVM ������ ��� ������ ���� �� ���θ� ������(true - ��� ���� ����)
sfa_dump_send_elapsed_ms | 30000 | �ڹ� ��ġ ���� �ð��� ���� ������ �ð� �̻��� ��쿡�� ��ī���� ������ ������ ���� �α׸� ������(�и���) 
batch_log_send_elapsed_ms | 30000 | �ڹ� ��ġ ���� �ð��� ���� ������ �ð� �̻��� ��쿡�� ��ī���� ������ ��ġ ���� ������ ������(�и���)
thread_check_interval_ms | 1000 | �ڹ� ��ġ ���ο� �����尡 ����Ǿ����� �ֱ������� üũ�ϴ� �ð�(�⺻: 1��). �ڹ� ��ġ ������Ʈ�� ������ ������ SQL ���� ��踦 �����ϴµ� �����尡 ����Ǹ� �ش� �������� ��踦 ��ü ��迡 �����ϴ� �۾��� ������. �̶� ������ ���� ���θ� Ȯ����
net_collector_ip | 127.0.0.1 | ��ī���� ���� IP �ּ�
net_collector_udp_port | 6100 | ��ī���� ������ UDP ���� Port ��ȣ
net_collector_tcp_port | 6100 | ��ī���� ������ TCP ��� Port ��ȣ
net_collector_tcp_session_count | 1 | ��ī���� ������ TCP ��� ���� ��
net_collector_tcp_so_timeout_ms | 60000 | ��ī���� ������ TCP ���� ���� �б� Ÿ�Ӿƿ� �ð�(�и���)
net_collector_tcp_connection_timeout_ms | 3000 | ��ī���� ������ TCP ���� ���� �б� Ÿ�Ӿƿ� �ð�(�и���)
net_local_udp_port | 6101 | ��ī���� �ڹ� ��ġ ������Ʈ�� UDP ��� Port. �� ��ġ ���μ����� ��ġ �������Ϳ� ���� �����͸� ������ �� ����ϴ� UDP ��Ʈ
net_udp_packet_max_bytes | 60000 | UDP ��� �� �ִ� ��Ŷ ũ��
obj_name | | �ڹ� ��ġ ���������� ��Ī(�⺻ ���� �����ϰ��� �� �� �����)
obj_host_type | | �ڹ� ��ġ�� �����ϴ� ������ Ÿ�� ����
obj_host_name | | �ڹ� ��ġ�� �����ϴ� ������ ȣ��Ʈ ���� ����(��ī���� ȣ��Ʈ ������Ʈ���� Obj_name�� ������ ��� �ش� ���� ���ο� �ִ� �� ������Ʈ�� �Ҽ� ȣ��Ʈ ���� �����ؾ� ��) 
_log_asm_enabled | false | ��ī���Ͱ� ����͸��� ���� ����Ʈ�ڵ� �����Ͼ�� ���������� �����ϴ��� ���θ� Ȯ���ϱ� ���� ����� ����(false - ����� ����)
log_dir | | �ڹ� ���� �α׿� �ܵ� ���� ��忡�� �����Ǵ� �ڹ� ���� ���� ��� ����(sbr)�� �����Ǵ� ���丮(�⺻�� �ڹ� ��ġ ������Ʈ ��ġ ���丮 �Ʒ� log ���丮) 
log_rotation_enabled | true | �ڹ� ��ġ ������Ʈ �α� ������ �ϴ����� �����Ͽ� �������� ���θ� ������(true - �ϴ��� �α� ����)
log_keep_days | 7 | �ڹ� ��ġ ������Ʈ �α׸� �����ϴ� �Ⱓ ����(��)


## �ڹ� ������Ʈ�� ������
��ī���� ��ġ ������Ʈ�� ��ī��Ʈ �ڹ� ������Ʈ�� �ٸ� ���� ��ġ ������Ʈ�� ��ġ�� ������ ���� ��ī���� ��ġ ������ ������Ѿ� �Ѵٴ� ���̴�.
�̴� ��ġ ���μ����� �׻� ���������� �ʰ�, ���ʰ� �̻� ���μ����� ���ÿ� �����ϱ� ������ �׻� ���� ���·� ��ġ ������ �����ϸ鼭 ��ġ ������Ʈ ȯ�漳���̳� ���� ���� ���� �� ������ ����� ���μ����� �ʿ��ϴ�.
��ī���� ��ġ ������ scouter.agent.batch.jar �� ���ԵǾ� �ִ�.

*start-batch-agent.sh*
```
nohup java -cp ${SCOUTER_AGENT_DIR}/scouter.agent.batch.jar -Dscouter.config=${SCOUTER_AGENT_DIR}/scouter.batch.conf scouter.agent.batch.Main &
```
***
��ī���� ��ġ ������ ������� ������ ��ġ Ŭ���̾�Ʈ���� ȯ�漳�� ����, ���� ����, ��ġ ���� ī��Ʈ ���� �� ����� ���� �������� �ʴ´�.

## ��ī���� ��ġ ����͸� ȭ��
![Scouter](../img/client/batch_monitor_example1.png)