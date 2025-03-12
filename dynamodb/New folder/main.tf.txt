module "dynamodb_table" {
  source      = "./module"
  table_name  = "my-dynamodb-table"
  hash_key    = "id"

  attributes = [
    { name = "id", type = "S" },
    { name = "created_at", type = "N" }
  ]

  billing_mode = "PAY_PER_REQUEST"

  global_secondary_indexes = [
    {
      name            = "created_at-index"
      hash_key        = "created_at"
      projection_type = "ALL"
    }
  ]

  ttl_enabled         = true
  ttl_attribute_name  = "expiration_time"

  point_in_time_recovery = true
  sse_enabled           = true

  tags = {
    Environment = "production"
    Project     = "example"
  }
}
