# Cloud 9 tools

# Hvordan øke diskplass til Cloud 9 

Det kan være en god idé å være proaktiv og øke lagringsplassen i Cloud9-miljøet. Dette kan oppnås ved hjelp av to kommandoer. Den første kommandoen utvider størrelsen på disken til EC2-instansen som Cloud9 kjører på.
Den andre kommandoen sørger for at operativsystemet har tilgang til den utvidede diskplassen.

```shell
aws ec2 modify-volume --volume-id $(aws ec2 describe-volumes --region $(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone | sed 's/[a-z]$//') --filters Name=attachment.instance-id,Values=$(curl -s http://169.254.169.254/latest/meta-data/instance-id) --query "Volumes[*].VolumeId" --output text) --size 20     
sudo growpart /dev/nvme0n1 1
```

# Om rettigheter i Cloud 9 

Når du åpner Cloud9 miljøet ditt, vil du få tildelt et lite sett med rettigheter som gir deg tilgang til de vanligste AWS tjenestene. 
Hvis du skal jobbe med andre tjenester, er det best å jobbe med sine egne IAM nøkler tilknyttet sin egen bruker. 

Jeg vil anbefale å opprette nøkler for din IAM bruker og kjøre ```aws configure``` fra Cloud9 i terminalen for å jobbe  
som en egen bruker.
