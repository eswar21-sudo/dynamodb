variable "table_name" {
  description = "Name of the DynamoDB table"
  type        = string
}

variable "billing_mode" {
  description = "Billing mode for the table (PROVISIONED or PAY_PER_REQUEST)"
  type        = string
  default     = "PAY_PER_REQUEST"
}

variable "hash_key" {
  description = "Hash key attribute name"
  type        = string
}

variable "range_key" {
  description = "Range key attribute name (optional)"
  type        = string
  default     = null
}

variable "attributes" {
  description = "List of attributes with name and type"
  type        = list(object({ name = string, type = string }))
}

variable "global_secondary_indexes" {
  description = "List of global secondary indexes"
  type = list(object({
    name            = string
    hash_key        = string
    range_key       = optional(string)
    projection_type = optional(string, "ALL")
    read_capacity   = optional(number)
    write_capacity  = optional(number)
  }))
  default = []
}

variable "local_secondary_indexes" {
  description = "List of local secondary indexes"
  type = list(object({
    name            = string
    range_key       = string
    projection_type = optional(string, "ALL")
  }))
  default = []
}

variable "ttl_attribute_name" {
  description = "TTL attribute name"
  type        = string
  default     = null
}

variable "ttl_enabled" {
  description = "Enable TTL for the table"
  type        = bool
  default     = false
}

variable "stream_enabled" {
  description = "Enable DynamoDB Streams"
  type        = bool
  default     = false
}

variable "stream_view_type" {
  description = "View type for streams"
  type        = string
  default     = null
}

variable "point_in_time_recovery" {
  description = "Enable Point-in-Time Recovery"
  type        = bool
  default     = false
}

variable "sse_enabled" {
  description = "Enable server-side encryption"
  type        = bool
  default     = true
}

variable "sse_kms_key_arn" {
  description = "KMS Key ARN for server-side encryption"
  type        = string
  default     = null
}

variable "tags" {
  description = "Tags for the DynamoDB table"
  type        = map(string)
  default     = {}
}
