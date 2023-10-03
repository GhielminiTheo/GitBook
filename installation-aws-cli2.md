---
description: Commandes pour l'installation et le configuration de AWS CLI2
---

# Installation AWS CLI2

Windows :&#x20;

Installation du CLI :

```
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
```

Vérification de l'installation du CLI :&#x20;

<pre><code><strong>[INPUT]
</strong><strong>aws --version
</strong><strong>[OUTPUT]
</strong>aws-cli/2.13.23 Python/3.11.5 Windows/10 exe/AMD64 prompt/off
</code></pre>

Lister les bucket&#x20;

<pre><code><strong>[INPUT]
</strong>aws s3 ls
[OUTPUT]
2023-10-03 11:14:55 guignard.diduno.education
2023-10-02 21:26:51 teacher.diduno.education
</code></pre>

Créer un bucket

```
[INPUT]
aws s3api create-bucket --bucket ghielmini.diduno.education --region eu-south-1 --create-bucket-configuration LocationConstraint=eu-south-1
[OUTPUT]
{
    "Location": "http://ghielmini.diduno.education.s3.amazonaws.com/"
}
```

Vérification de la présence du bucket&#x20;

```
[INPUT]
aws s3 ls
[OUTPUT]
2023-10-03 11:33:32 deoliveiracalhau.diduno.education
2023-10-03 11:34:22 ghielmini.diduno.education
2023-10-03 11:14:55 guignard.diduno.education
2023-10-03 11:25:56 mayor.diduno.education
2023-10-03 11:29:55 moser.diduno.education
2023-10-02 21:26:51 teacher.diduno.education
```

Copier un objet vers le bucket

<pre><code><strong>[INPUT]
</strong><strong>aws s3 cp E:\Test.txt s3://ghielmini.diduno.education
</strong>[OUTPUT]
upload: E:\Test.txt to s3://ghielmini.diduno.education/Test.txt
</code></pre>

Récupérer un objet sur le bucket vers la machine windows

```
[INPUT]
aws s3 cp s3://ghielmini.diduno.education/Test.txt E:\

[OUTPUT]
download: s3://ghielmini.diduno.education/Test.txt to E:\Test.txt
```

Positionner  (PAS SUR de cette commande)

```
[INPUT]
aws s3 cp E:\Test.txt s3://ghielmini.diduno.education/MyFolder
[OUTPUT]
upload: E:\Test.txt to s3://ghielmini.diduno.education/MyFolder
```

Supprimer un objet

<pre><code>[INPUT]
<strong>aws s3api delete-object --bucket ghielmini.diduno.education --key Test.txt
</strong>
[OUTPUT]
aws s3api delete-object --bucket ghielmini.diduno.education --key Test.txt
rien ne s'affiche
</code></pre>

<pre><code><strong>[INPUT]
</strong><strong>aws s3 rm s3://ghielmini.diduno.education/Test.txt
</strong><strong>[OUTPUT]
</strong>delete: s3://ghielmini.diduno.education/Test.txt
</code></pre>
