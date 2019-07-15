**======================== Local(Using DirectRunner) ============================

mvn compile -e exec:java \
 -Dexec.mainClass=com.raj.processor.DQ \
      -Dexec.args="--project=<YOUR_PROJECT_NAME> \
      --stagingLocation=gs://<YOUR_BUCKET_NAME>/staging/ \
      --tempLocation=gs://<YOUR_BUCKET_NAME>/staging/ \
      --input=gs://<YOUR_BUCKET_NAME>/data/day_1.csv \
  	  --output=gs://<YOUR_BUCKET_NAME>/data/complete_output/  \
      --inputType=csv \
      --outputType=csv  \
      --cdcType="scdtype2" \
      --goodRecordPath=gs://<YOUR_BUCKET_NAME>/data/staging \
      --errorPath=gs://<YOUR_BUCKET_NAME>/data/badrecords/ \
      --configName=gs://<YOUR_BUCKET_NAME>/data/original_config.properties \
      --dqOutputType=csv"


*======================== On Google cloud (using DataflowRunner) ============================
mvn compile -e exec:java  -Dexec.mainClass=com.raj.processor.DQ       -Dexec.args="--proje
ct=<YOUR_PROJECT_NAME> \
      --stagingLocation=gs://<YOUR_BUCKET_NAME>/staging/ \
      --tempLocation=gs://<YOUR_BUCKET_NAME>/staging/ \
      --input=gs://<YOUR_BUCKET_NAME>/data/day_1.csv \
    --output=gs://<YOUR_BUCKET_NAME>/data/complete_output/  \
      --inputType=csv \
      --outputType=csv  \
      --cdcType="scdtype2" \
      --goodRecordPath=gs://<YOUR_BUCKET_NAME>/data/staging \
      --errorPath=gs://<YOUR_BUCKET_NAME>/data/badrecords/ \
      --configName=gs://<YOUR_BUCKET_NAME>/data/original_config.properties \
      --dqOutputType=csv \
      --runner=DataflowRunner"

      
 * On Hadoop cluster (using SparkRunner)
 
spark-submit --master local[*] --class com.raj.processor.IngestParquet /Users/raj/git/b-for-beam/processor/target/processor-0.0.1-SNAPSHOT.jar --runner=SparkRunner  --input=/Users/raj/git/b-for-beam/processor/src/main/resources/data/day_2.csv --output=/Users/raj/git/b-for-beam/processor/src/main/resources/data/complete_output/ --inputType=csv --outputType=csv  --cdcType="scdtype2" --goodRecordPath=/Users/raj/git/b-for-beam/processor/src/main/resources/data/staging/ --errorPath=/Users/raj/git/b-for-beam/processor/src/main/resources/data/badrecords/ --configName=/Users/raj/git/b-for-beam/processor/src/main/resources/data/original_config.properties --dqOutputType=csv