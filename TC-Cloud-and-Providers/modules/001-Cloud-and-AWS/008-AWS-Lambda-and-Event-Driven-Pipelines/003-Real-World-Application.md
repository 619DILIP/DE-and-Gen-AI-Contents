## Automating a Partner Data Feed

A company receives sales files from several retail partners, uploaded at unpredictable times throughout the day. Before automation, someone checked for new files each morning and ran a processing script by hand, meaning data was up to a day stale and the process failed silently when that person was away.

Replacing this with an event driven pipeline changes the shape of the problem. Partners upload to an S3 bucket. Each upload triggers a Lambda function that validates the file, standardizes the format differences between partners, and writes the records into the warehouse. Data is available within seconds of arrival, nothing runs when no files are coming in, and there is no server to maintain.

The failure handling also improves. A malformed file from one partner causes that single invocation to fail and be logged, while files from every other partner continue processing normally. Under the previous approach, one bad file could stop the whole morning's run.