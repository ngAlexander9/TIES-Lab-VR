# Cloud Compare Process

Using office-setting dataset

- Load into Cloudcompare
  - might lag out, so try to only have 1 scan visible at a time to reduce rendering load
- select desired scan
- Select segment tool (scissors in toolbar)
  - Use segment tool to select desired points
  - Click segment in 
  - Click Check mark to confirm
  - Delete .remaining points
  - Repeat for all scans
- Select all prepared scans
  - Edit -> Merge
  - Scans should combine into one scan file
- Compute Normals
  - Edit -> Normals -> Compute
  - In orientation, make sure use sensors whenever possible is checked and select use preferred orientation -> sensor origin
  - Takes a while to calculate (went not responding for me a couple times)
- Poisson
- 
